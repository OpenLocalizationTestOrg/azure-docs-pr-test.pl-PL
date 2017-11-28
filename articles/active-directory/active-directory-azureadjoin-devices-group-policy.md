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
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="a3940-103">Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="a3940-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="a3940-104">Przyłączanie do domeny jest organizacje tradycyjny sposób połączyły urządzenia do pracy w ciągu ostatnich 15 lat i inne.</span><span class="sxs-lookup"><span data-stu-id="a3940-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="a3940-105">Ma ona włączone użytkownikom logowania się na urządzeniach przy użyciu ich pracy Windows Server Active Directory (Active Directory) lub konta służbowego i dozwolone IT do pełnego zarządzania tymi urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="a3940-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="a3940-106">Organizacje zazwyczaj są oparte na metodach obrazu, aby zainicjować obsługę administracyjną urządzeń do użytkowników i zazwyczaj Użyj programu System Center Configuration Manager (SCCM) lub zasad grupy do zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="a3940-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="a3940-107">Przyłączanie do domeny w systemie Windows 10 zapewnia następujące korzyści po podłączeniu urządzenia do usługi Azure Active Directory (Azure AD):</span><span class="sxs-lookup"><span data-stu-id="a3940-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="a3940-108">Logowanie jednokrotne (SSO) do zasobów usługi Azure AD z dowolnego miejsca</span><span class="sxs-lookup"><span data-stu-id="a3940-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="a3940-109">Dostęp do przedsiębiorstwa Sklepu Windows przy użyciu kont służbowych (nie wymagane konto Microsoft)</span><span class="sxs-lookup"><span data-stu-id="a3940-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="a3940-110">Zgodne Enterprise roaming ustawień użytkownika na urządzeniach przy użyciu kont służbowych (nie wymagane konto Microsoft)</span><span class="sxs-lookup"><span data-stu-id="a3940-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="a3940-111">Silne uwierzytelnianie i wygodne logowanie dla konta służbowego z usługi Windows Hello dla firm i usługi Windows Hello</span><span class="sxs-lookup"><span data-stu-id="a3940-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="a3940-112">Możliwość ograniczenia dostępu tylko do urządzeń, które są zgodne z ustawieniami zasad grupy organizacyjnej urządzenia</span><span class="sxs-lookup"><span data-stu-id="a3940-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3940-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a3940-113">Prerequisites</span></span>
<span data-ttu-id="a3940-114">Przyłączanie do domeny jest nadal użyteczne.</span><span class="sxs-lookup"><span data-stu-id="a3940-114">Domain join continues to be useful.</span></span> <span data-ttu-id="a3940-115">Jednak aby uzyskać korzyści usługi Azure AD z logowania jednokrotnego, roaming ustawień z pracy lub kont służbowych i dostęp do Sklepu Windows przy użyciu kont służbowych, potrzebne będą następujące:</span><span class="sxs-lookup"><span data-stu-id="a3940-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="a3940-116">Subskrypcja usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3940-116">Azure AD subscription</span></span>
* <span data-ttu-id="a3940-117">Azure AD Connect, aby rozszerzyć katalog lokalny z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3940-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="a3940-118">Zasady, które ma ustawioną wartość podłączania urządzeń przyłączonych do domeny do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3940-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="a3940-119">Kompilacji systemu Windows 10 (kompilacja 10551 lub nowsza) dla urządzeń</span><span class="sxs-lookup"><span data-stu-id="a3940-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="a3940-120">Aby włączyć usługi Windows Hello dla firm i usługi Windows Hello, również potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a3940-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="a3940-121">**Infrastruktury kluczy publicznych (PKI)** do wystawiania certyfikatów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a3940-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="a3940-122">**System Center Configuration Manager Current Branch** — należy zainstalować wersję 1606 lub większą.</span><span class="sxs-lookup"><span data-stu-id="a3940-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="a3940-123">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="a3940-123">For more information, see:</span></span> 
    - [<span data-ttu-id="a3940-124">Dokumentacja programu System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a3940-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="a3940-125">Blog zespołu programu System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a3940-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="a3940-126">Usługi Windows Hello dla firm ustawień w programie System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a3940-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="a3940-127">Jako alternatywę do wymagań wdrażania infrastruktury kluczy publicznych należy wykonać następujące:</span><span class="sxs-lookup"><span data-stu-id="a3940-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="a3940-128">Mają kilka kontrolerów domeny z systemem Windows Server 2016 usług domenowych Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a3940-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="a3940-129">Aby włączyć dostęp warunkowy, można utworzyć ustawień zasad grupy, które umożliwiają dostęp do urządzeń przyłączonych do domeny z nie dodatkowe wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a3940-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="a3940-130">Aby zarządzać kontrola dostępu oparta na zgodności urządzenia, potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a3940-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="a3940-131">System Center Configuration Manager Current Branch (1606 lub nowszego) dla usługi Windows Hello dla różnych scenariuszy biznesowych</span><span class="sxs-lookup"><span data-stu-id="a3940-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="a3940-132">Instrukcje dotyczące wdrażania</span><span class="sxs-lookup"><span data-stu-id="a3940-132">Deployment instructions</span></span>

<span data-ttu-id="a3940-133">Aby wdrożyć, wykonaj czynności opisane w [Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="a3940-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="a3940-134">Następny krok</span><span class="sxs-lookup"><span data-stu-id="a3940-134">Next step</span></span>
* [<span data-ttu-id="a3940-135">System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy</span><span class="sxs-lookup"><span data-stu-id="a3940-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="a3940-136">Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="a3940-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="a3940-137">Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="a3940-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="a3940-138">Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="a3940-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="a3940-139">Konfigurowanie funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="a3940-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

