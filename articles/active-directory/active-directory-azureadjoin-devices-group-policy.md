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
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="fe58a-103">Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="fe58a-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="fe58a-104">Przyłączanie do domeny jest hello tradycyjny sposób organizacji połączyły urządzenia do pracy nad hello ostatnich 15 lat i inne.</span><span class="sxs-lookup"><span data-stu-id="fe58a-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="fe58a-105">Włączono toosign użytkowników na urządzeniach tootheir przy użyciu ich pracy Windows Server Active Directory (Active Directory) lub konta służbowego i dozwolonych toofully IT zarządzać tymi urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="fe58a-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="fe58a-106">Organizacje są zwykle oparte na imaging metody tooprovision urządzeń toousers i toomanage programu System Center Configuration Manager (SCCM) lub zasad grupy na ogół służy je.</span><span class="sxs-lookup"><span data-stu-id="fe58a-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="fe58a-107">Przyłączanie do domeny w systemie Windows 10 zapewnia powitania po podłączeniu urządzenia tooAzure usługi Active Directory (Azure AD), następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="fe58a-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="fe58a-108">Pojedynczy logowania jednokrotnego (SSO) tooAzure AD zasobów z dowolnego miejsca</span><span class="sxs-lookup"><span data-stu-id="fe58a-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="fe58a-109">Dostęp do przedsiębiorstwa toohello Sklepu Windows przy użyciu pracy lub szkołą kont (nie wymagane konto Microsoft)</span><span class="sxs-lookup"><span data-stu-id="fe58a-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="fe58a-110">Zgodne Enterprise roaming ustawień użytkownika na urządzeniach przy użyciu kont służbowych (nie wymagane konto Microsoft)</span><span class="sxs-lookup"><span data-stu-id="fe58a-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="fe58a-111">Silne uwierzytelnianie i wygodne logowanie dla konta służbowego z usługi Windows Hello dla firm i usługi Windows Hello</span><span class="sxs-lookup"><span data-stu-id="fe58a-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="fe58a-112">Toorestrict możliwość dostępu tylko toodevices, które są zgodne z ustawieniami zasad grupy organizacyjnej urządzenia</span><span class="sxs-lookup"><span data-stu-id="fe58a-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe58a-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fe58a-113">Prerequisites</span></span>
<span data-ttu-id="fe58a-114">Przyłączanie do domeny nadal toobe przydatne.</span><span class="sxs-lookup"><span data-stu-id="fe58a-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="fe58a-115">Jednak tooget hello Azure AD zalet logowania jednokrotnego, roaming ustawień z lub szkolnego konta i do uzyskiwania dostępu do magazynu tooWindows pracy służbowe kont, konieczne będzie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="fe58a-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="fe58a-116">Subskrypcja usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe58a-116">Azure AD subscription</span></span>
* <span data-ttu-id="fe58a-117">Azure AD Connect tooextend hello lokalnego katalogu tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="fe58a-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="fe58a-118">Zasady, które ustawił tooconnect tooAzure urządzeń przyłączonych do domeny usługi AD</span><span class="sxs-lookup"><span data-stu-id="fe58a-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="fe58a-119">Kompilacji systemu Windows 10 (kompilacja 10551 lub nowsza) dla urządzeń</span><span class="sxs-lookup"><span data-stu-id="fe58a-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="fe58a-120">tooenable Windows Hello dla firm i Windows Hello, należy również hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fe58a-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="fe58a-121">**Infrastruktury kluczy publicznych (PKI)** do wystawiania certyfikatów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe58a-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="fe58a-122">**System Center Configuration Manager Current Branch** — wymagana wersja tooinstall 1606 lub większą.</span><span class="sxs-lookup"><span data-stu-id="fe58a-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="fe58a-123">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="fe58a-123">For more information, see:</span></span> 
    - [<span data-ttu-id="fe58a-124">Dokumentacja programu System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="fe58a-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="fe58a-125">Blog zespołu programu System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="fe58a-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="fe58a-126">Usługi Windows Hello dla firm ustawień w programie System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="fe58a-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="fe58a-127">Jako alternatywne toohello wymagania wdrożenia infrastruktury kluczy publicznych, wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="fe58a-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="fe58a-128">Mają kilka kontrolerów domeny z systemem Windows Server 2016 usług domenowych Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe58a-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="fe58a-129">dostęp warunkowy tooenable, można utworzyć ustawień zasad grupy, które umożliwiają dostęp do urządzeń przyłączonych do toodomain z nie dodatkowe wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fe58a-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="fe58a-130">toomanage kontrola dostępu oparta na zgodności urządzenia hello, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="fe58a-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="fe58a-131">System Center Configuration Manager Current Branch (1606 lub nowszego) dla usługi Windows Hello dla różnych scenariuszy biznesowych</span><span class="sxs-lookup"><span data-stu-id="fe58a-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="fe58a-132">Instrukcje dotyczące wdrażania</span><span class="sxs-lookup"><span data-stu-id="fe58a-132">Deployment instructions</span></span>

<span data-ttu-id="fe58a-133">toodeploy, wykonaj kroki hello na liście [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="fe58a-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="fe58a-134">Następny krok</span><span class="sxs-lookup"><span data-stu-id="fe58a-134">Next step</span></span>
* [<span data-ttu-id="fe58a-135">System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy</span><span class="sxs-lookup"><span data-stu-id="fe58a-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="fe58a-136">Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="fe58a-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="fe58a-137">Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="fe58a-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="fe58a-138">Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="fe58a-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="fe58a-139">Konfigurowanie funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="fe58a-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

