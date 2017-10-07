---
title: "scenariusze aaaAdvanced z usługi Azure MFA i sieci VPN innych firm"
description: "Przewodniki krok po kroku konfiguracji dla usługi Azure MFA toointegrate Cisco, Citrix i Juniper."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Scenariusze Zaawansowane z usługi Azure Multi-Factor Authentication i rozwiązania sieci VPN innych firm
Usługa Azure Multi-Factor Authentication może służyć tooseamlessly Uzyskuj dostęp do różnych rozwiązań sieci VPN innych firm. Ten artykuł dotyczy urządzenia sieci VPN ASA® Cisco, Citrix NetScaler SSL sieci VPN urządzenia i hello Juniper sieci bezpieczny dostęp/Pulse Secure połączenie Secure SSL urządzenia sieci VPN. Utworzyliśmy tooaddress przewodniki konfiguracji tych trzech wspólnych urządzeń, ale serwer Multi-Factor Authentication można zintegrować z większością systemów, które używają usługi RADIUS, LDAP, usługi IIS lub uwierzytelniania opartego na oświadczeniach tooAD FS. Szczegółowe informacje można znaleźć [konfiguracji serwera usługi MFA](multi-factor-authentication-get-started-server.md#next-steps).

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Cisco ASA sieci VPN urządzenia i uwierzytelnianie wieloskładnikowe Azure
Uwierzytelnianie wieloskładnikowe platformy Azure jest zintegrowany z Cisco® ASA VPN urządzenia tooprovide dodatkowe zabezpieczenia logowania Cisco AnyConnect® VPN i dostępu do portalu.  Można to zrobić przy użyciu albo hello protokołu LDAP lub serwera RADIUS.  Wybierz jedną z hello zgodnie szczegółową konfigurację krok hello toodownload prowadzi.

| Przewodnik po konfiguracji | Opis |
| --- | --- |
| [Cisco ASA z Anyconnect sieci VPN i usługi Azure MFA konfiguracji LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | Integracja z usługą Azure MFA przy użyciu protokołu LDAP urządzenia Cisco ASA VPN |
| [Cisco ASA z Anyconnect sieci VPN i usługi Azure MFA konfiguracji usługi RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | Integracja z urządzenia Cisco ASA VPN z usługą Azure MFA korzystanie z usługi RADIUS |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>Citrix NetScaler SSL sieci VPN i usługi Azure Multi-Factor Authentication
Uwierzytelnianie wieloskładnikowe platformy Azure jest zintegrowany z Citrix NetScaler SSL sieci VPN urządzenia tooprovide dodatkowe zabezpieczenia logowania Citrix NetScaler SSL sieci VPN i dostępu do portalu.  Można to zrobić przy użyciu albo hello protokołu LDAP lub serwera RADIUS.  Wybierz jedną z hello zgodnie szczegółową konfigurację krok hello toodownload prowadzi.

| Przewodnik po konfiguracji | Opis |
| --- | --- |
| [Citrix NetScaler SSL sieci VPN i usługi Azure MFA konfiguracji LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | Integracja programu Citrix NetScaler SSL sieci VPN z urządzenia usługi Azure MFA przy użyciu protokołu LDAP |
| [Citrix NetScaler SSL sieci VPN i usługi Azure MFA konfiguracji usługi RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | Integracja z usługą Azure MFA korzystanie z usługi RADIUS urządzenia Citrix NetScaler SSL sieci VPN |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Urządzenia juniper/Pulse Secure VPN protokołu SSL i uwierzytelnianie wieloskładnikowe Azure
Usługa Azure Multi-Factor Authentication integruje się z sieci VPN protokołu SSL Juniper/Pulse Secure urządzenia tooprovide dodatkowe zabezpieczenia logowania Juniper/Pulse Secure SSL VPN i dostępu do portalu.  Można to zrobić przy użyciu albo hello protokołu LDAP lub serwera RADIUS.  Wybierz jedną z hello zgodnie szczegółową konfigurację krok hello toodownload prowadzi.

| Przewodnik po konfiguracji | Opis |
| --- | --- |
| [Juniper/Pulse bezpiecznego VPN protokołu SSL i usługi Azure MFA konfiguracji LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | Integracja z Juniper/Pulse Secure SSL sieci VPN z urządzenia usługi Azure MFA przy użyciu protokołu LDAP |
| [Juniper/Pulse bezpiecznego VPN protokołu SSL i usługi Azure MFA konfiguracji usługi RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | Integracja z usługą Azure MFA korzystanie z usługi RADIUS urządzenia Juniper/Pulse Secure VPN protokołu SSL |

## <a name="next-steps"></a>Następne kroki

- [Rozszerzyć istniejącą infrastrukturę uwierzytelniania z hello rozszerzenia serwera NPS uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-nps-extension.md)

- [Konfigurowanie ustawień usługi Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md)