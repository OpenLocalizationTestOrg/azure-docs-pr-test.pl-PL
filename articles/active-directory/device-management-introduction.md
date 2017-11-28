---
title: "aaaIntroduction toodevice zarządzania w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzanie urządzeniami może pomóc tooget kontrola nad urządzeniami hello, które uzyskują dostęp do zasobów w danym środowisku."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="73072-103">Wprowadzenie toodevice zarządzania w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73072-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="73072-104">W świecie pierwszy mobile, najpierw chmury Azure Active Directory (Azure AD) umożliwia toodevices rejestracji jednokrotnej, aplikacji i usług z dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="73072-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="73072-105">Z hello mnożenie urządzeń — łącznie z urządzenia (PRZYNIEŚ własne) specjalistów IT muszą stawiać czoła dwóch celów przeciwna:</span><span class="sxs-lookup"><span data-stu-id="73072-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="73072-106">Zwiększenie możliwości dostępnych dla toobe użytkownicy końcowi hello produktywności wszędzie tam, gdzie i po każdej zmianie</span><span class="sxs-lookup"><span data-stu-id="73072-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="73072-107">Ochrona zasobów firmowych hello w dowolnym momencie</span><span class="sxs-lookup"><span data-stu-id="73072-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="73072-108">Za pomocą urządzeń użytkownicy są uzyskiwania dostępu tooyour zasobów firmowych.</span><span class="sxs-lookup"><span data-stu-id="73072-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="73072-109">tooprotect z zasobami firmy jako IT administrator chcesz toohave kontrolę nad tymi urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="73072-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="73072-110">Dzięki temu toomake się upewnić, że użytkownicy uzyskują dostęp do zasobów z urządzeń, które spełniają standardy zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="73072-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="73072-111">Zarządzanie urządzeniami jest również podstawą hello [dostępu warunkowego opartego na urządzeniu](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="73072-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="73072-112">Przy użyciu dostępu warunkowego opartego na urządzeniach można zapewnić, że dostępu tooresources w danym środowisku jest możliwe za pomocą tylko zaufane urządzenia.</span><span class="sxs-lookup"><span data-stu-id="73072-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="73072-113">W tym temacie wyjaśniono, jak działa zarządzanie urządzeniami w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73072-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="73072-114">Pobieranie urządzeń pod kontrolą hello usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73072-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="73072-115">tooget urządzenie pod kontrolą hello usługi Azure AD, dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="73072-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="73072-116">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="73072-116">Registering</span></span> 
- <span data-ttu-id="73072-117">Łączenie</span><span class="sxs-lookup"><span data-stu-id="73072-117">Joining</span></span>

<span data-ttu-id="73072-118">**Rejestrowanie** tooAzure urządzenia AD umożliwia możesz toomanage tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="73072-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="73072-119">Po zarejestrowaniu urządzenia rejestracji urządzeń usługi Azure AD zapewnia hello urządzenia przy użyciu tożsamości, która jest używana tooauthenticate hello urządzenia, gdy tooAzure loguje użytkownika AD.</span><span class="sxs-lookup"><span data-stu-id="73072-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="73072-120">Można użyć tooenable tożsamości hello lub wyłącz urządzenie.</span><span class="sxs-lookup"><span data-stu-id="73072-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="73072-121">W połączeniu z rozwiązaniem management(MDM) urządzeń przenośnych, takich jak Microsoft Intune, dodatkowe informacje o urządzeniu hello są aktualizowane hello atrybutów urządzenia w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73072-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="73072-122">Dzięki temu można toocreate zasady dostępu warunkowego, które wymuszają dostęp z urządzeń toomeet standardy zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="73072-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="73072-123">Aby uzyskać więcej informacji dotyczących rejestrowania urządzeń w Microsoft Intune Zobacz rejestrowanie urządzeń do zarządzania w usłudze Intune.</span><span class="sxs-lookup"><span data-stu-id="73072-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="73072-124">**Sprzęganie** urządzenie jest tooregistering rozszerzenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="73072-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="73072-125">Oznacza to, zapewnia ona wszystkich funkcji hello rejestrowania urządzenia i w dodatku toothis, również zmiany stanu lokalne powitania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="73072-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="73072-126">Zmiana stanu lokalne powitania umożliwia urządzenie toosign w tooa użytkowników przy użyciu organizacji konta firmowego lub szkolnego, zamiast konta osobistego.</span><span class="sxs-lookup"><span data-stu-id="73072-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="73072-127">Urządzenia zarejestrowane usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73072-127">Azure AD registered devices</span></span>   

<span data-ttu-id="73072-128">Witaj celem urządzeń usługi Azure AD w zarejestrowany jest tooprovide o obsługę hello **urządzenia (PRZYNIEŚ własne)** scenariusza.</span><span class="sxs-lookup"><span data-stu-id="73072-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="73072-129">W tym scenariuszu użytkownik mógł korzystać z zasobów usługi Azure Active Directory pod kontrolą firmy za pomocą urządzeń osobistych.</span><span class="sxs-lookup"><span data-stu-id="73072-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Urządzenia zarejestrowane usługi Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="73072-131">Witaj dostępu jest oparty na konta firmowego lub szkolnego, który został wprowadzony na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="73072-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="73072-132">Na przykład systemu Windows 10 umożliwia tooadd użytkownikom pracy lub komputerów osobistych tooa konto służbowe, tabletu lub telefonu.</span><span class="sxs-lookup"><span data-stu-id="73072-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="73072-133">Gdy użytkownik został dodany pracy lub konta służbowego, urządzenia hello jest zarejestrowana w usłudze Azure AD i opcjonalnie zarejestrowane w systemie zarządzania urządzeniami Przenośnymi na urządzenie przenośne hello, skonfigurowanego w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="73072-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="73072-134">Użytkowników w organizacji można dodać służbowego lub szkolnego konta tooa osobiste urządzenie wygodny sposób:</span><span class="sxs-lookup"><span data-stu-id="73072-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="73072-135">Podczas uzyskiwania dostępu do aplikacji pracy dla powitania po raz pierwszy</span><span class="sxs-lookup"><span data-stu-id="73072-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="73072-136">Ręcznie za pośrednictwem hello **ustawienia** menu w przypadku hello systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="73072-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="73072-137">Możesz skonfigurować urządzenia usługi Azure AD w zarejestrowany dla systemu Windows 10, iOS, Android i macOS.</span><span class="sxs-lookup"><span data-stu-id="73072-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="73072-138">Urządzeniach przyłączonych do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73072-138">Azure AD joined devices</span></span>

<span data-ttu-id="73072-139">Celem Hello urządzeń usługi Azure AD przyłączony jest toosimplify:</span><span class="sxs-lookup"><span data-stu-id="73072-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="73072-140">Wdrażanie systemu Windows urządzenia należące do pracy</span><span class="sxs-lookup"><span data-stu-id="73072-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="73072-141">Dostęp tooorganizational aplikacje i zasoby na dowolnym urządzeniu z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="73072-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Urządzenia zarejestrowane usługi Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="73072-143">Te cele są osiągane przez zapewnienie użytkownikom przy użyciu środowiska samoobsługi dla pobierania urządzenia należące do pracy pod kontrolą hello usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73072-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="73072-144">**Azure AD Join** jest przeznaczona dla organizacji, które są najpierw chmury / tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="73072-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="73072-145">Są to zazwyczaj małych i średnich firm, które nie mają infrastruktury lokalnej usługi Active Directory systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="73072-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="73072-146">Wdrażanie usługi Azure AD przyłączone do urządzeń zawiera hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="73072-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="73072-147">**Single-Sign-On rejestracji jednokrotnej (SSO)** tooyour Azure zarządzanych usług i aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="73072-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="73072-148">Użytkownicy nie zobaczą monity o dodatkowe uwierzytelnianie podczas uzyskiwania dostępu do zasobów roboczych.</span><span class="sxs-lookup"><span data-stu-id="73072-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="73072-149">Hello funkcji rejestracji Jednokrotnej jest parzysta, gdy nie są one dostępnych sieci połączonych toohello domeny.</span><span class="sxs-lookup"><span data-stu-id="73072-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="73072-150">**Roaming zgodne Enterprise** ustawień użytkownika na urządzeniach połączonych.</span><span class="sxs-lookup"><span data-stu-id="73072-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="73072-151">Użytkownicy nie muszą tooconnect toosee ustawienia konta (na przykład usługi Hotmail) firmy Microsoft na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="73072-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="73072-152">**Dostęp tooWindows sklepu dla firm** przy użyciu konta usługi AD.</span><span class="sxs-lookup"><span data-stu-id="73072-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="73072-153">Użytkownicy, można wybrać ze spisu aplikacji wstępnie wybrany przez organizację hello.</span><span class="sxs-lookup"><span data-stu-id="73072-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="73072-154">**Usługi Windows Hello** obsługę dostęp do bezpiecznego i wygodne toowork zasobów.</span><span class="sxs-lookup"><span data-stu-id="73072-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="73072-155">**Ograniczenie dostępu** tooapps z tylko w przypadku urządzeń, które spełniają zasady zgodności.</span><span class="sxs-lookup"><span data-stu-id="73072-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="73072-156">Podczas usługi Azure AD join jest przeznaczone głównie dla organizacji, które nie mają infrastruktury lokalnej usługi Active Directory systemu Windows Server, można wykonywać następujące czynności na pewno również korzystać w scenariuszach, w których:</span><span class="sxs-lookup"><span data-stu-id="73072-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="73072-157">Przyłączanie do domeny lokalnej nie można użyć na przykład, jeśli potrzebujesz tooget urządzeń przenośnych, takich jak tablety i telefony pod kontrolą.</span><span class="sxs-lookup"><span data-stu-id="73072-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="73072-158">Użytkownicy potrzebują głównie tooaccess usługi Office 365 lub innych aplikacji SaaS zintegrowanych z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73072-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="73072-159">Ma toomanage grupy użytkowników w usłudze Azure AD, a nie w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73072-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="73072-160">Może to dotyczyć, na przykład tooseasonal pracownicy, wykonawcy lub studentów.</span><span class="sxs-lookup"><span data-stu-id="73072-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="73072-161">Ma tooprovide łącząca tooworkers możliwości w biurach oddziałów zdalnego z infrastruktury lokalnej ograniczone.</span><span class="sxs-lookup"><span data-stu-id="73072-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="73072-162">Możesz skonfigurować urządzenia usługi Azure AD połączone dla urządzeń z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="73072-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="73072-163">Urządzeniach przyłączonych do hybrydowej usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73072-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="73072-164">Przez ponad dekadę w wielu organizacjach używanych hello domeny sprzężenia tootheir lokalnej usługi Active Directory tooenable:</span><span class="sxs-lookup"><span data-stu-id="73072-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="73072-165">IT działów toomanage pracy urządzeń należących do firmy z centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="73072-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="73072-166">Toosign użytkowników na urządzeniach tootheir z ich Active Directory służbowe kont.</span><span class="sxs-lookup"><span data-stu-id="73072-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="73072-167">Zazwyczaj organizacji mających wpływ na lokalnym zależne od metod tooprovision urządzenia do obrazowania, a często używane **programu System Center Configuration Manager (SCCM)** lub **(GP) zasad grupy** toomanage je.</span><span class="sxs-lookup"><span data-stu-id="73072-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="73072-168">Jeśli środowisko ma lokalnego wpływ AD, a także korzyści z hello możliwości oferowane przez usługi Azure Active Directory, można zaimplementować hybrydowe usługi Azure AD przyłączone do urządzeń.</span><span class="sxs-lookup"><span data-stu-id="73072-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="73072-169">Są to urządzenia, które są, tooyour dołączonego do lokalnej usługi Active Directory i Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73072-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Urządzenia zarejestrowane usługi Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="73072-171">Należy używać urządzeń hybrydowego przyłączonych do usługi Azure AD, jeśli:</span><span class="sxs-lookup"><span data-stu-id="73072-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="73072-172">Urządzeń toothese wdrożonej aplikacji Win32, korzystających z protokołu NTLM / Kerberos.</span><span class="sxs-lookup"><span data-stu-id="73072-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="73072-173">Wymagaj zasad grupy lub SCCM / DCM toomanage urządzeń.</span><span class="sxs-lookup"><span data-stu-id="73072-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="73072-174">Chcesz toocontinue toouse obrazowania rozwiązań tooconfigure urządzenia dla pracowników.</span><span class="sxs-lookup"><span data-stu-id="73072-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="73072-175">Można skonfigurować hybrydowe usługi Azure AD urządzeniach przyłączonych do systemu Windows 10 i urządzeniach niskiego poziomu, takich jak Windows 8 i Windows 7.</span><span class="sxs-lookup"><span data-stu-id="73072-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="73072-176">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="73072-176">Summary</span></span>

<span data-ttu-id="73072-177">Zarządzanie urządzeniami w usłudze Azure AD możesz:</span><span class="sxs-lookup"><span data-stu-id="73072-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="73072-178">Uprościć proces hello zapewniania urządzeń pod kontrolą hello usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="73072-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="73072-179">Zapewnić użytkownikom łatwe toouse dostępu tooyour organizacji zasobów w chmurze</span><span class="sxs-lookup"><span data-stu-id="73072-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="73072-180">Zgodnie z zasadą thumb należy użyć:</span><span class="sxs-lookup"><span data-stu-id="73072-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="73072-181">Usługi Azure AD zarejestrowane urządzenia dla urządzeń osobistych</span><span class="sxs-lookup"><span data-stu-id="73072-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="73072-182">Przyłączone urządzeń do usługi Azure AD dla urządzeń, które nie są przyłączone do tooan lokalnej usłudze AD</span><span class="sxs-lookup"><span data-stu-id="73072-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="73072-183">Hybrydowe usługi Azure AD przyłączone urządzeń dla urządzeń, które są przyłączone do tooan lokalnej usłudze AD</span><span class="sxs-lookup"><span data-stu-id="73072-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="73072-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73072-184">Next steps</span></span>

- <span data-ttu-id="73072-185">tooget jak urządzenie toomanage hello Azure portalu, zobacz Omówienie [zarządzanie urządzeniami za pomocą hello portalu Azure](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="73072-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="73072-186">toolearn więcej informacji na temat dostępu warunkowego opartego na urządzeniu, zobacz [Konfigurowanie zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="73072-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="73072-187">toosetup hybrydowe usługi Azure AD przyłączone do urządzenia, zobacz [jak tooconfigure hybrydowe usługi Azure Active Directory łączone urządzeń](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="73072-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


