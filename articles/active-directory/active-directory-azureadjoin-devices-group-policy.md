---
title: "napotyka aaaConnect tooAzure urządzeń przyłączonych do domeny usługi AD w systemie Windows 10 | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak Administratorzy mogą skonfigurować sieci przedsiębiorstwa przyłączonych do domeny toohello toobe urządzeń tooenable zasad grupy."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10
Przyłączanie do domeny jest hello tradycyjny sposób organizacji połączyły urządzenia do pracy nad hello ostatnich 15 lat i inne. Włączono toosign użytkowników na urządzeniach tootheir przy użyciu ich pracy Windows Server Active Directory (Active Directory) lub konta służbowego i dozwolonych toofully IT zarządzać tymi urządzeniami. Organizacje są zwykle oparte na imaging metody tooprovision urządzeń toousers i toomanage programu System Center Configuration Manager (SCCM) lub zasad grupy na ogół służy je.


Przyłączanie do domeny w systemie Windows 10 zapewnia powitania po podłączeniu urządzenia tooAzure usługi Active Directory (Azure AD), następujące korzyści:

* Pojedynczy logowania jednokrotnego (SSO) tooAzure AD zasobów z dowolnego miejsca
* Dostęp do przedsiębiorstwa toohello Sklepu Windows przy użyciu pracy lub szkołą kont (nie wymagane konto Microsoft)
* Zgodne Enterprise roaming ustawień użytkownika na urządzeniach przy użyciu kont służbowych (nie wymagane konto Microsoft)
* Silne uwierzytelnianie i wygodne logowanie dla konta służbowego z usługi Windows Hello dla firm i usługi Windows Hello
* Toorestrict możliwość dostępu tylko toodevices, które są zgodne z ustawieniami zasad grupy organizacyjnej urządzenia

## <a name="prerequisites"></a>Wymagania wstępne
Przyłączanie do domeny nadal toobe przydatne. Jednak tooget hello Azure AD zalet logowania jednokrotnego, roaming ustawień z lub szkolnego konta i do uzyskiwania dostępu do magazynu tooWindows pracy służbowe kont, konieczne będzie hello następujące:

* Subskrypcja usługi Azure AD
* Azure AD Connect tooextend hello lokalnego katalogu tooAzure AD
* Zasady, które ustawił tooconnect tooAzure urządzeń przyłączonych do domeny usługi AD
* Kompilacji systemu Windows 10 (kompilacja 10551 lub nowsza) dla urządzeń

tooenable Windows Hello dla firm i Windows Hello, należy również hello następujące czynności:

- **Infrastruktury kluczy publicznych (PKI)** do wystawiania certyfikatów użytkownika.

- **System Center Configuration Manager Current Branch** — wymagana wersja tooinstall 1606 lub większą.  
Aby uzyskać więcej informacji, zobacz: 
    - [Dokumentacja programu System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [Blog zespołu programu System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Usługi Windows Hello dla firm ustawień w programie System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Jako alternatywne toohello wymagania wdrożenia infrastruktury kluczy publicznych, wykonaj następujące hello:

* Mają kilka kontrolerów domeny z systemem Windows Server 2016 usług domenowych Active Directory.

dostęp warunkowy tooenable, można utworzyć ustawień zasad grupy, które umożliwiają dostęp do urządzeń przyłączonych do toodomain z nie dodatkowe wdrożenia. toomanage kontrola dostępu oparta na zgodności urządzenia hello, potrzebne są następujące hello:

* System Center Configuration Manager Current Branch (1606 lub nowszego) dla usługi Windows Hello dla różnych scenariuszy biznesowych

## <a name="deployment-instructions"></a>Instrukcje dotyczące wdrażania

toodeploy, wykonaj kroki hello na liście [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Następny krok
* [System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

