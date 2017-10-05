---
title: "Łączenie urządzeń przyłączonych do domeny do usługi Azure AD dla systemu Windows 10 napotyka | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak Administratorzy mogą skonfigurować zasady grupy, aby włączyć urządzeń przyłączonych do domeny w sieci przedsiębiorstwa."
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a>Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10
Przyłączanie do domeny jest organizacje tradycyjny sposób połączyły urządzenia do pracy w ciągu ostatnich 15 lat i inne. Ma ona włączone użytkownikom logowania się na urządzeniach przy użyciu ich pracy Windows Server Active Directory (Active Directory) lub konta służbowego i dozwolone IT do pełnego zarządzania tymi urządzeniami. Organizacje zazwyczaj są oparte na metodach obrazu, aby zainicjować obsługę administracyjną urządzeń do użytkowników i zazwyczaj Użyj programu System Center Configuration Manager (SCCM) lub zasad grupy do zarządzania nimi.


Przyłączanie do domeny w systemie Windows 10 zapewnia następujące korzyści po podłączeniu urządzenia do usługi Azure Active Directory (Azure AD):

* Logowanie jednokrotne (SSO) do zasobów usługi Azure AD z dowolnego miejsca
* Dostęp do przedsiębiorstwa Sklepu Windows przy użyciu kont służbowych (nie wymagane konto Microsoft)
* Zgodne Enterprise roaming ustawień użytkownika na urządzeniach przy użyciu kont służbowych (nie wymagane konto Microsoft)
* Silne uwierzytelnianie i wygodne logowanie dla konta służbowego z usługi Windows Hello dla firm i usługi Windows Hello
* Możliwość ograniczenia dostępu tylko do urządzeń, które są zgodne z ustawieniami zasad grupy organizacyjnej urządzenia

## <a name="prerequisites"></a>Wymagania wstępne
Przyłączanie do domeny jest nadal użyteczne. Jednak aby uzyskać korzyści usługi Azure AD z logowania jednokrotnego, roaming ustawień z pracy lub kont służbowych i dostęp do Sklepu Windows przy użyciu kont służbowych, potrzebne będą następujące:

* Subskrypcja usługi Azure AD
* Azure AD Connect, aby rozszerzyć katalog lokalny z usługą Azure AD
* Zasady, które ma ustawioną wartość podłączania urządzeń przyłączonych do domeny do usługi Azure AD
* Kompilacji systemu Windows 10 (kompilacja 10551 lub nowsza) dla urządzeń

Aby włączyć usługi Windows Hello dla firm i usługi Windows Hello, również potrzebne następujące elementy:

- **Infrastruktury kluczy publicznych (PKI)** do wystawiania certyfikatów użytkownika.

- **System Center Configuration Manager Current Branch** — należy zainstalować wersję 1606 lub większą.  
Aby uzyskać więcej informacji, zobacz: 
    - [Dokumentacja programu System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [Blog zespołu programu System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Usługi Windows Hello dla firm ustawień w programie System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Jako alternatywę do wymagań wdrażania infrastruktury kluczy publicznych należy wykonać następujące:

* Mają kilka kontrolerów domeny z systemem Windows Server 2016 usług domenowych Active Directory.

Aby włączyć dostęp warunkowy, można utworzyć ustawień zasad grupy, które umożliwiają dostęp do urządzeń przyłączonych do domeny z nie dodatkowe wdrożenia. Aby zarządzać kontrola dostępu oparta na zgodności urządzenia, potrzebne następujące elementy:

* System Center Configuration Manager Current Branch (1606 lub nowszego) dla usługi Windows Hello dla różnych scenariuszy biznesowych

## <a name="deployment-instructions"></a>Instrukcje dotyczące wdrażania

Aby wdrożyć, wykonaj czynności opisane w [Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Następny krok
* [System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

