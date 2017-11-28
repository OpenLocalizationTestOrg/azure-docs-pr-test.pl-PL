---
title: "niższego poziomu urządzeniach przyłączonych do aaaTroubleshooting hybrydowe usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z hybrydowe usługi Azure Active Directory połączone urządzenia niższego poziomu."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="3fc46-103">Rozwiązywanie problemów z hybrydowe usługi Azure Active Directory przyłączone do urządzeń niskiego poziomu</span><span class="sxs-lookup"><span data-stu-id="3fc46-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="3fc46-104">Ten temat jest stosowane tylko toohello następujące urządzenia:</span><span class="sxs-lookup"><span data-stu-id="3fc46-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="3fc46-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="3fc46-105">Windows 7</span></span> 
- <span data-ttu-id="3fc46-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3fc46-106">Windows 8.1</span></span> 
- <span data-ttu-id="3fc46-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3fc46-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="3fc46-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3fc46-108">Windows Server 2012</span></span> 
- <span data-ttu-id="3fc46-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3fc46-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="3fc46-110">Dla systemu Windows 10 lub Windows Server 2016, zobacz [hybrydowego Rozwiązywanie problemów z usługą Azure Active Directory przyłączone do urządzeń z systemem Windows 10 i Windows Server 2016](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="3fc46-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="3fc46-111">W tym temacie założono, że [urządzeniach przyłączonych do skonfigurowanego hybrydowe usługi Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="3fc46-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="3fc46-112">Dostępu warunkowego opartego na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="3fc46-112">Device-based conditional access</span></span>

- [<span data-ttu-id="3fc46-113">Enterprise roaming ustawień</span><span class="sxs-lookup"><span data-stu-id="3fc46-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="3fc46-114">Windows Hello dla firm</span><span class="sxs-lookup"><span data-stu-id="3fc46-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="3fc46-115">Ten temat zawiera rozwiązania wskazówki dotyczące sposobu tooresolve potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="3fc46-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="3fc46-116">**Co należy wiedzieć:**</span><span class="sxs-lookup"><span data-stu-id="3fc46-116">**What you should know:**</span></span> 

- <span data-ttu-id="3fc46-117">Witaj maksymalną liczbę urządzeń dla każdego użytkownika jest perspektywy skoncentrowanej na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="3fc46-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="3fc46-118">Na przykład jeśli *jdoe* i *jharnett* urządzenia tooa logowania, rejestracji odrębnych (DeviceID) jest tworzony dla każdego z nich w hello **użytkownika** kartę informacje.</span><span class="sxs-lookup"><span data-stu-id="3fc46-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="3fc46-119">Witaj początkowe rejestracyjny / join urządzeń jest skonfigurowany tooperform próba logowania lub lock / odblokowania.</span><span class="sxs-lookup"><span data-stu-id="3fc46-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="3fc46-120">Mogą wystąpić opóźnienia 5-minutowy wyzwalane przez zadania harmonogramu zadań.</span><span class="sxs-lookup"><span data-stu-id="3fc46-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="3fc46-121">Ponowna instalacja systemu operacyjnego hello lub ręcznego unregister i wykonaj ponowną rejestrację może utworzyć nowej rejestracji w usłudze Azure AD i powoduje wiele wpisów hello użytkownika informacje o karcie w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc46-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="3fc46-122">Krok 1: Pobierz hello stan rejestracji</span><span class="sxs-lookup"><span data-stu-id="3fc46-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="3fc46-123">**Stan rejestracji hello tooverify:**</span><span class="sxs-lookup"><span data-stu-id="3fc46-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="3fc46-124">Witaj Otwórz wiersz polecenia jako administrator</span><span class="sxs-lookup"><span data-stu-id="3fc46-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="3fc46-125">Typ`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="3fc46-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="3fc46-126">To polecenie wyświetla okno dialogowe, która udostępnia szczegółowe informacje o stanie sprzężenia hello.</span><span class="sxs-lookup"><span data-stu-id="3fc46-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="3fc46-128">Krok 2: Ocena hello hybrydowe usługi Azure AD join stanu</span><span class="sxs-lookup"><span data-stu-id="3fc46-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="3fc46-129">Jeśli hello hybrydowe usługi Azure AD join zakończyła się niepowodzeniem, okno dialogowe hello zawiera szczegółowe informacje o problemie hello, który wystąpił.</span><span class="sxs-lookup"><span data-stu-id="3fc46-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="3fc46-130">**najbardziej typowe problemy Hello są:**</span><span class="sxs-lookup"><span data-stu-id="3fc46-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="3fc46-131">Nieprawidłowej konfiguracji usług AD FS lub Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fc46-131">A misconfigured AD FS or Azure AD</span></span>

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="3fc46-133">Użytkownik nie jest zarejestrowany jako użytkownik domeny</span><span class="sxs-lookup"><span data-stu-id="3fc46-133">You are not signed on as a domain user</span></span>

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="3fc46-135">Osiągnięto limit przydziału</span><span class="sxs-lookup"><span data-stu-id="3fc46-135">A quota has been reached</span></span>

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="3fc46-137">Usługa Hello nie odpowiada</span><span class="sxs-lookup"><span data-stu-id="3fc46-137">hello service is not responding</span></span> 

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="3fc46-139">Informacje o stanie hello również można znaleźć w dzienniku zdarzeń hello w obszarze **aplikacji i usług Log\Microsoft-dołączania**.</span><span class="sxs-lookup"><span data-stu-id="3fc46-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="3fc46-140">**Najczęstszymi przyczynami sprzężenia usługi Azure AD nie powiodło się hybrydowego Hello są:**</span><span class="sxs-lookup"><span data-stu-id="3fc46-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="3fc46-141">Twój komputer nie jest w sieci wewnętrznej hello organizacji lub sieci VPN bez tooan połączenia lokalnego kontrolera domeny AD.</span><span class="sxs-lookup"><span data-stu-id="3fc46-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="3fc46-142">Użytkownik jest zalogowany tooyour komputera przy użyciu konta komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="3fc46-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="3fc46-143">Problemy z konfiguracją usługi:</span><span class="sxs-lookup"><span data-stu-id="3fc46-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="3fc46-144">Witaj serwer federacyjny został skonfigurowany toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="3fc46-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="3fc46-145">Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje tooyour zweryfikowaną nazwę domeny w usłudze Azure AD w lesie hello AD, której należy komputer hello.</span><span class="sxs-lookup"><span data-stu-id="3fc46-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="3fc46-146">Użytkownik osiągnął limit hello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="3fc46-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3fc46-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3fc46-147">Next steps</span></span>

<span data-ttu-id="3fc46-148">Odpowiedzi na pytania, zobacz hello [zarządzanie urządzeniami — często zadawane pytania](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3fc46-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
