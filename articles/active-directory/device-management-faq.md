---
title: "aaaAzure zarządzania urządzeniami w usłudze Active Directory — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Azure Active Directory Zarządzanie urządzeniami — często zadawane pytania."
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
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="39335-103">Zarządzanie urządzeniami w usłudze Azure Active Directory — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="39335-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="39335-104">**Pytanie: czy mogę ostatnio zarejestrowany hello urządzenia. Dlaczego nie widzę hello urządzenia w obszarze Moje informacje użytkownika w portalu Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="39335-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="39335-105">**Odpowiedź:** urządzeń z systemem Windows 10, które są przyłączone do domeny z automatycznej rejestracji urządzeń nie są wyświetlane w obszarze hello informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="39335-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="39335-106">Należy toouse PowerShell toosee wszystkie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="39335-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="39335-107">Tylko hello następujące urządzenia są wyświetlane w obszarze informacje o użytkowniku hello:</span><span class="sxs-lookup"><span data-stu-id="39335-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="39335-108">Wszystkich urządzeń osobistych, które nie są przyłączone do przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="39335-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="39335-109">Wszystkie z systemem innym niż Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="39335-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="39335-110">Wszystkie urządzenia z systemem innym niż Windows</span><span class="sxs-lookup"><span data-stu-id="39335-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="39335-111">**Pytanie: Dlaczego nie można wyświetlić wszystkie urządzenia hello zarejestrowane w usłudze Azure Active Directory w portalu Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="39335-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="39335-112">**Odpowiedź:** nie istnieje aktualnie nie toosee sposób wszystkich zarejestrowanych urządzeń w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="39335-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="39335-113">Można użyć programu Azure PowerShell toofind wszystkie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="39335-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="39335-114">Aby uzyskać więcej informacji, zobacz hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="39335-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="39335-115">**Pytanie: jak sprawdzić, jakie stan rejestracji urządzenia hello powitania klienta jest?**</span><span class="sxs-lookup"><span data-stu-id="39335-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="39335-116">**Odpowiedź:** zależy od stanu rejestracji urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="39335-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="39335-117">Jakie urządzenia hello jest</span><span class="sxs-lookup"><span data-stu-id="39335-117">What hello device is</span></span>
- <span data-ttu-id="39335-118">Jak został zarejestrowany</span><span class="sxs-lookup"><span data-stu-id="39335-118">How it was registered</span></span> 
- <span data-ttu-id="39335-119">Szczegółowe informacje dotyczące tooit.</span><span class="sxs-lookup"><span data-stu-id="39335-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="39335-120">**Pytanie: Dlaczego jest to urządzenie I usunięto w hello Azure portalu lub przy użyciu programu Windows PowerShell nadal wymieniony jako zarejestrowane?**</span><span class="sxs-lookup"><span data-stu-id="39335-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="39335-121">**Odpowiedź:** to jest celowe.</span><span class="sxs-lookup"><span data-stu-id="39335-121">**A:** This is by design.</span></span> <span data-ttu-id="39335-122">Witaj urządzenie nie będzie miał tooresources dostęp w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="39335-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="39335-123">Jeśli mają tooremove hello urządzenia i zarejestrować go ponownie, akcji ręcznej musi być toobe wykonywaną na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="39335-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="39335-124">Dla systemu Windows 10 i Windows Server 2016, które są lokalne AD przyłączonych do domeny:</span><span class="sxs-lookup"><span data-stu-id="39335-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="39335-125">Witaj Otwórz wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="39335-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="39335-126">Typ`dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="39335-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="39335-127">Wyloguj się i zaloguj się tootrigger hello zaplanowane zadanie, które rejestruje urządzenie hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="39335-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="39335-128">Dla innych platform systemu Windows, które znajdują się na obszarze AD przyłączonych do domeny:</span><span class="sxs-lookup"><span data-stu-id="39335-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="39335-129">Witaj Otwórz wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="39335-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="39335-130">Wpisz polecenie `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="39335-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="39335-131">Wpisz polecenie `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="39335-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="39335-132">**Pytanie: Dlaczego Zobacz urządzenia zduplikowanych wpisów w portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="39335-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="39335-133">**ODP.:**</span><span class="sxs-lookup"><span data-stu-id="39335-133">**A:**</span></span>

-   <span data-ttu-id="39335-134">Dla systemu Windows 10 i Windows Server 2016, jeśli są toounjoin kolejnych nieudanych prób i ponownie Dołącz hello tego samego urządzenia, może być w niej zduplikowanych pozycji.</span><span class="sxs-lookup"><span data-stu-id="39335-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="39335-135">Jeśli używasz konta Dodaj firmowego lub szkolnego każdego użytkownika systemu windows, który używa konta Dodaj firmowego lub szkolnego utworzy nowy rekord urządzenia hello tę samą nazwę urządzenia.</span><span class="sxs-lookup"><span data-stu-id="39335-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="39335-136">Inne platformy systemu Windows, które znajdują się na obszarze AD przyłączonych do domeny za pomocą automatycznej rejestracji utworzy nowy rekord urządzenia z hello tę samą nazwę urządzenia dla każdego użytkownika domeny, który loguje się do hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="39335-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="39335-137">AADJ maszynę, która została wyczyszczona, ponowna instalacja i ponownie połączony z hello takie same nazwy, będzie wyświetlany jako inny rekord z hello tę samą nazwę urządzenia.</span><span class="sxs-lookup"><span data-stu-id="39335-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="39335-138">**Pytanie: Dlaczego użytkownik nadal dostęp do zasobów z urządzenia I zostały wyłączone w portalu Azure hello?**</span><span class="sxs-lookup"><span data-stu-id="39335-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="39335-139">**Odpowiedź:** może potrwać godzinę tooan toobe odwołania, stosowane.</span><span class="sxs-lookup"><span data-stu-id="39335-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="39335-140">Utracone urządzeń zaleca się czyszczenie hello urządzenia tooensure, że użytkownicy nie mają dostępu hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="39335-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="39335-141">Aby uzyskać więcej informacji, zobacz [rejestrowanie urządzeń do zarządzania w usłudze Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="39335-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="39335-142">**Pytanie: Dlaczego Moi użytkownicy widzą "Nie można pobrać istnieje w tym miejscu"?**</span><span class="sxs-lookup"><span data-stu-id="39335-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="39335-143">**Odpowiedź:** hello urządzenie nie spełnia kryteriów hello skonfigurowano niektórych toorequire zasady dostępu warunkowego stanu określonego urządzenia, użytkownicy są blokowane, a ten komunikat zostanie wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="39335-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="39335-144">Sprawdź oszacowanie reguł hello i upewnij się, czy urządzenie hello jest możliwe toomeet hello kryteria tooavoid tego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="39335-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="39335-145">**Pytanie: Zobacz hello rekordem urządzenia w obszarze hello informacje o użytkowniku w portalu Azure hello i widoczny stan hello zarejestrowany na powitania klienta. Czy prawidłowo skonfigurować do korzystania z dostępu warunkowego?**</span><span class="sxs-lookup"><span data-stu-id="39335-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="39335-146">**Odpowiedź:** hello rekord urządzenia (deviceID) i stan na powitania portalu Azure musi odpowiada powitania klienta i spełniać wszystkie kryteria oceny dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="39335-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="39335-147">Aby uzyskać więcej informacji, zobacz [wprowadzenie do rejestracji urządzeń usługi Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="39335-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="39335-148">**Pytanie: Dlaczego jest wyświetlany jest komunikat "Nazwa użytkownika lub hasło jest niepoprawne" urządzenia I po prostu dołączeniu tooAzure AD?**</span><span class="sxs-lookup"><span data-stu-id="39335-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="39335-149">**Odpowiedź:** są typowe przyczyny tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="39335-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="39335-150">Poświadczenia użytkownika nie są już prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="39335-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="39335-151">Ten komputer jest toocommunicate w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="39335-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="39335-152">Sprawdź, czy wszystkie problemy z połączeniem sieciowym.</span><span class="sxs-lookup"><span data-stu-id="39335-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="39335-153">Hello Azure AD Join wymagania wstępne nie zostały spełnione.</span><span class="sxs-lookup"><span data-stu-id="39335-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="39335-154">Upewnij się, że zostały wykonane kroki hello [rozszerzanie możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join chmury](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39335-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="39335-155">Logowania federacyjnego wymaga programu toosupport serwera federacyjnego aktywny punkt końcowy protokołu WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="39335-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="39335-156">**Pytanie: Dlaczego Zobacz hello "Oops... Wystąpił błąd!" okna dialogowego podczas próby dołączenia komputera?**</span><span class="sxs-lookup"><span data-stu-id="39335-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="39335-157">**Odpowiedź:** jest to wynik konfigurowania rejestracji usługi Azure Active Directory z usługą Intune.</span><span class="sxs-lookup"><span data-stu-id="39335-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="39335-158">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zarządzania urządzeniami z systemem Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="39335-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="39335-159">**Pytanie: Dlaczego moja toojoin próba komputer się nie powieść, mimo że uzyskane informacje o błędzie?**</span><span class="sxs-lookup"><span data-stu-id="39335-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="39335-160">**Odpowiedź:** prawdopodobną przyczyną jest hello jest on zalogowany w toohello urządzenia przy użyciu hello wbudowanego konta administratora.</span><span class="sxs-lookup"><span data-stu-id="39335-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="39335-161">Przed rozpoczęciem korzystania z usługi Azure Active Directory Join toocomplete hello Instalator, Utwórz innego konta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="39335-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="39335-162">**Pytanie: gdzie można znaleźć instrukcje instalacji hello automatycznej rejestracji urządzeń?**</span><span class="sxs-lookup"><span data-stu-id="39335-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="39335-163">**A:** szczegółowe instrukcje, zobacz [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="39335-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="39335-164">**Pytanie: gdzie mogę znaleźć, rozwiązywanie problemów z informacji o hello automatycznej rejestracji urządzeń?**</span><span class="sxs-lookup"><span data-stu-id="39335-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="39335-165">**Odpowiedź:** informacje dotyczące rozwiązywania problemów, zobacz:</span><span class="sxs-lookup"><span data-stu-id="39335-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="39335-166">Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — Windows 10 i Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="39335-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="39335-167">Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD dla klientów niższego poziomu z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="39335-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

