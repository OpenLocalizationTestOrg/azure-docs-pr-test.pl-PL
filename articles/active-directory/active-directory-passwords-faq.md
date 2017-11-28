---
title: "Często zadawane pytania: Azure AD SSPR | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi Azure AD samoobsługi hasła resetowania"
services: active-directory
keywords: "Zarządzanie hasłami w usłudze Active directory, zarządzanie hasłami, usługi Azure AD samodzielnego resetowania hasła usługi"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="1f349-104">Często zadawane pytania dotyczące zarządzania hasłami</span><span class="sxs-lookup"><span data-stu-id="1f349-104">Password management frequently asked questions</span></span>

<span data-ttu-id="1f349-105">powitania po są niektóre często zadawane pytania wszystkich czynności związanych z toopassword resetowania.</span><span class="sxs-lookup"><span data-stu-id="1f349-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="1f349-106">Jeśli masz pytania ogólne dotyczące usługi Azure AD i hasło samodzielnego resetowania, który nie ma odpowiedzi w tym miejscu, można zadawać społeczności hello pomocy na powitania [fora usługi Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="1f349-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="1f349-107">Członkowie społeczności hello obejmują Engineers, menedżerów produktu MVP i twarzy specjalistów IT.</span><span class="sxs-lookup"><span data-stu-id="1f349-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="1f349-108">Często zadawane pytania jest podzielony na powitania następujące sekcje:</span><span class="sxs-lookup"><span data-stu-id="1f349-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="1f349-109">**Pytania dotyczące rejestracji resetowania hasła**</span><span class="sxs-lookup"><span data-stu-id="1f349-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="1f349-110">**Pytania dotyczące resetowania hasła**</span><span class="sxs-lookup"><span data-stu-id="1f349-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="1f349-111">**Pytania dotyczące zmiany hasła**</span><span class="sxs-lookup"><span data-stu-id="1f349-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="1f349-112">**Raporty pytania dotyczące zarządzania hasłami**</span><span class="sxs-lookup"><span data-stu-id="1f349-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="1f349-113">**Pytania dotyczące funkcji zapisywania zwrotnego haseł**</span><span class="sxs-lookup"><span data-stu-id="1f349-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="1f349-114">Rejestracja resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="1f349-114">Password reset registration</span></span>
* <span data-ttu-id="1f349-115">**Pytanie: czy Moi użytkownicy rejestrowanie własnych danych resetowania hasła?**</span><span class="sxs-lookup"><span data-stu-id="1f349-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="1f349-116">**Odpowiedź:** tak, jak długo resetowania hasła jest włączona i są one licencjonowane, mogą one portalu rejestracji resetowania haseł toohello pod adresem http://aka.ms/ssprsetup tooregister ich informacje dotyczące uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1f349-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="1f349-117">Użytkownicy mogą również zarejestrować przez przechodzi do panelu dostępu toohello pod adresem http://myapps.microsoft.com, klikając kartę profil hello, a polecenie hello rejestru dla opcji resetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="1f349-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="1f349-118">**Q: czy można zdefiniować dane resetowania hasła w imieniu użytkowników?**</span><span class="sxs-lookup"><span data-stu-id="1f349-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="1f349-119">**Odpowiedź:** tak, możesz to zrobić z hello Azure AD Connect, programu PowerShell, [portalu Azure](https://portal.azure.com), lub portalu administracyjnego Office hello.</span><span class="sxs-lookup"><span data-stu-id="1f349-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="1f349-120">Aby uzyskać więcej informacji, zobacz artykuł hello [dane używane przez usługi Azure AD samoobsługowego resetowania hasła](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="1f349-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="1f349-121">**Pytanie: czy można synchronizować dane odpowiedzi na pytania zabezpieczające z lokalnie?**</span><span class="sxs-lookup"><span data-stu-id="1f349-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="1f349-122">**Odpowiedź:** nie jest to możliwe dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="1f349-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="1f349-123">**Pytanie: czy Moi użytkownicy zarejestrować danych w taki sposób, że inni użytkownicy nie widzą te dane?**</span><span class="sxs-lookup"><span data-stu-id="1f349-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="1f349-124">**Odpowiedź:** tak, gdy użytkownicy zarejestrować danych do pól prywatnych uwierzytelniania, które są widoczne przez użytkownika administratorzy globalni i hello tylko przy użyciu hello portalu resetowania haseł rejestracji jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="1f349-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="1f349-125">Jeśli **konto administratora platformy Azure** rejestruje numer telefonu uwierzytelniania również są umieszczane w pole telefonu komórkowego hello i jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="1f349-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="1f349-126">**Pytanie: czy Moi użytkownicy mają toobe zarejestrowane przed użyciem resetowania hasła?**</span><span class="sxs-lookup"><span data-stu-id="1f349-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="1f349-127">**Odpowiedź:** nie, jeśli zdefiniujesz wystarczających informacji uwierzytelniania w ich imieniu użytkownicy nie mają tooregister.</span><span class="sxs-lookup"><span data-stu-id="1f349-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="1f349-128">Działania resetowania hasła, tak długo, jak długo mają poprawnie sformatowana danych przechowywanych w hello odpowiednich pól w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="1f349-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="1f349-129">**Pytanie: można zsynchronizować lub ustawiają pola numer telefonu uwierzytelniania, uwierzytelniania wiadomości E-mail lub alternatywny numer telefonu uwierzytelniania hello imieniu mojej użytkowników?**</span><span class="sxs-lookup"><span data-stu-id="1f349-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="1f349-130">**Odpowiedź:** nie jest to możliwe dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="1f349-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="1f349-131">**Pytanie: jak portalu rejestracji hello wiedzieć, który tooshow opcje Moi użytkownicy?**</span><span class="sxs-lookup"><span data-stu-id="1f349-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="1f349-132">**Odpowiedź:** portalu rejestracji resetowania haseł hello programu tylko pokazuje hello opcje, które zostały włączone dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1f349-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="1f349-133">Te opcje można znaleźć w obszarze hello sekcji zasady resetowania hasła użytkownika karta Konfigurowanie w katalogu. Na przykład oznacza to, że jeśli pytania zabezpieczające nie jest włączona, następnie użytkownicy nie są możliwe tooregister dla tej opcji.</span><span class="sxs-lookup"><span data-stu-id="1f349-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="1f349-134">**Pytanie: Jeśli użytkownik jest uznawany zarejestrowane?**</span><span class="sxs-lookup"><span data-stu-id="1f349-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="1f349-135">**A:** użytkownik jest uznawany w zarejestrowany dla usługi SSPR, gdy zarejestrowanych co najmniej hello **liczbę metod wymagane tooreset** ustawioną w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f349-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="1f349-136">Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="1f349-136">Password reset</span></span>
* <span data-ttu-id="1f349-137">**Pytanie: jak długo powinna czekać tooreceive wiadomości e-mail, SMS lub połączeń telefonicznych z resetowania hasła?**</span><span class="sxs-lookup"><span data-stu-id="1f349-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="1f349-138">**Odpowiedź:** poczty E-mail, wiadomości SMS i połączeń telefonicznych powinno nastąpić w obszarze jedną minutę, z normalna sytuacja hello 5-20 sekund.</span><span class="sxs-lookup"><span data-stu-id="1f349-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="1f349-139">Jeśli w tym czasie nie jest wyświetlany hello powiadomień:</span><span class="sxs-lookup"><span data-stu-id="1f349-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="1f349-140">Sprawdź folder wiadomości-śmieci.</span><span class="sxs-lookup"><span data-stu-id="1f349-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="1f349-141">Sprawdź hello numer lub adres e-mail jest nawiązywane połączenie jest hello, co oczekiwane.</span><span class="sxs-lookup"><span data-stu-id="1f349-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="1f349-142">Sprawdź, czy dane uwierzytelniania hello w katalogu hello jest poprawnie sformatowana.</span><span class="sxs-lookup"><span data-stu-id="1f349-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="1f349-143">Przykład: "+ 1 4255551234" lub "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="1f349-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="1f349-144">**Pytanie: jakie języki są obsługiwane przez resetowania hasła?**</span><span class="sxs-lookup"><span data-stu-id="1f349-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="1f349-145">**Odpowiedź:** hello resetowania hasła interfejsu użytkownika, wiadomości SMS i głosu wywołania są zlokalizowane w hello te same języki, które są obsługiwane w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="1f349-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="1f349-146">**Karta na konfigurowanie Q: części środowisko resetowania hasła hello uzyskać marki, gdy ustawić organizacji znakowania w katalogu Moje?**</span><span class="sxs-lookup"><span data-stu-id="1f349-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="1f349-147">**Odpowiedź:** portal resetowania haseł hello pokazuje logo organizacji i pozwala hello tooconfigure kontakt e-mail administratora łącze toopoint tooa niestandardowych lub adres URL.</span><span class="sxs-lookup"><span data-stu-id="1f349-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="1f349-148">Każdej wiadomości e-mail, które są wysyłane przez resetowania haseł obejmuje logo organizacji, kolory, nazwy w treści hello hello poczty e-mail i dostosować na podstawie nazwy.</span><span class="sxs-lookup"><span data-stu-id="1f349-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="1f349-149">**Pytanie: jak Poinformuj użytkowników o tym, gdzie toogo tooreset swoje hasła?**</span><span class="sxs-lookup"><span data-stu-id="1f349-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="1f349-150">**A:** toohttps://passwordreset.microsoftonline.com Twojego użytkowników może wysyłać bezpośrednio lub polecić je tooclick hello **nie ma dostępu do konta łącze** na dowolnej pracy lub nauki strony logowania.</span><span class="sxs-lookup"><span data-stu-id="1f349-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="1f349-151">Można również opublikować te linki użytkownicy tooyour łatwo dostępne miejsce.</span><span class="sxs-lookup"><span data-stu-id="1f349-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="1f349-152">**Pytanie: czy można użyć tej strony z urządzenia przenośnego?**</span><span class="sxs-lookup"><span data-stu-id="1f349-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="1f349-153">**Odpowiedź:** tak, ta strona działa na urządzeniach przenośnych.</span><span class="sxs-lookup"><span data-stu-id="1f349-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="1f349-154">**Pytanie: czy odblokowywanie kont z lokalnej usługi active directory są obsługiwane podczas użytkownikom resetowania swoich haseł w?**</span><span class="sxs-lookup"><span data-stu-id="1f349-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="1f349-155">**Odpowiedź:** tak, gdy użytkownik resetuje hasła i zapisywania zwrotnego haseł został wdrożony za pomocą usługi Azure AD Connect, konto użytkownika jest odblokowany automatycznie podczas resetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="1f349-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="1f349-156">**Pytanie: jak można zintegrować resetowania bezpośrednio do mojego użytkownika logowania środowisko pulpitu**</span><span class="sxs-lookup"><span data-stu-id="1f349-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="1f349-157">**Odpowiedź:** w przypadku klienta programu Azure AD Premium można zainstalować programu Microsoft Identity Manager bez ponoszenia dodatkowych kosztów i wdrożyć hello lokalnego hasła resetowania rozwiązania toomeet to wymaganie.</span><span class="sxs-lookup"><span data-stu-id="1f349-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="1f349-158">**Pytanie: czy można ustawić pytania zabezpieczeń dla różnych ustawień regionalnych?**</span><span class="sxs-lookup"><span data-stu-id="1f349-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="1f349-159">**Odpowiedź:** nie jest to możliwe dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="1f349-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="1f349-160">**Pytanie: jak wiele pytań możemy skonfigurować dla opcji uwierzytelniania pytania zabezpieczające hello?**</span><span class="sxs-lookup"><span data-stu-id="1f349-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="1f349-161">**Odpowiedź:** too20 pytania zabezpieczające niestandardowych w hello skonfigurowaniem [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f349-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="1f349-162">**Pytanie: jak długo może być pytania zabezpieczające?**</span><span class="sxs-lookup"><span data-stu-id="1f349-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="1f349-163">**Odpowiedź:** pytania zabezpieczające może mieć długość od 3 do 200 znaków.</span><span class="sxs-lookup"><span data-stu-id="1f349-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="1f349-164">**Pytanie: jak długo może być toosecurity odpowiedzi na pytania?**</span><span class="sxs-lookup"><span data-stu-id="1f349-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="1f349-165">**Odpowiedź:** odpowiedzi może być 3 too40 znaków.</span><span class="sxs-lookup"><span data-stu-id="1f349-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="1f349-166">**Pytanie: czy odrzucony zduplikowane odpowiedzi na pytania toosecurity?**</span><span class="sxs-lookup"><span data-stu-id="1f349-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="1f349-167">**Odpowiedź:** tak, możemy Odrzuć toosecurity zduplikowane odpowiedzi na pytania.</span><span class="sxs-lookup"><span data-stu-id="1f349-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="1f349-168">**Pytanie: czy maja rejestru użytkownika hello tego samego pytanie zabezpieczające więcej niż raz?**</span><span class="sxs-lookup"><span data-stu-id="1f349-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="1f349-169">**Odpowiedź:** nie, gdy użytkownik rejestruje dane pytanie, ich nie może zarejestrować dla tego zapytania po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="1f349-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="1f349-170">**Pytanie: czy jest możliwe tooset minimalny limit pytania zabezpieczające w celu rejestracji i resetowania?**</span><span class="sxs-lookup"><span data-stu-id="1f349-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="1f349-171">**Odpowiedź:** tak, można ustawić limit jeden dla rejestracji i drugi dla resetowania.</span><span class="sxs-lookup"><span data-stu-id="1f349-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="1f349-172">pytania zabezpieczające 3 – 5 może być wymagany w czasie rejestracji i 3 – 5 mogą być wymagane w celu resetowania.</span><span class="sxs-lookup"><span data-stu-id="1f349-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="1f349-173">**Pytanie: Jeśli użytkownik został zarejestrowany w więcej niż maksymalna liczba pytań wymaganych tooreset hello, jak są pytania zabezpieczające wybrane podczas resetowania?**</span><span class="sxs-lookup"><span data-stu-id="1f349-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="1f349-174">**A:** zabezpieczeń N pytania są losowo wybrane poza hello łącznej liczby pytań, a użytkownik został zarejestrowany, gdzie N to hello **liczba pytań wymaganych tooreset**.</span><span class="sxs-lookup"><span data-stu-id="1f349-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="1f349-175">Na przykład jeśli użytkownik ma 5 pytania zabezpieczające w zarejestrowany, ale tooreset wymagane są tylko 3, 3 hello 5 są wybierane losowo i przedstawionego na resetowanie.</span><span class="sxs-lookup"><span data-stu-id="1f349-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="1f349-176">Jeśli hello użytkownik otrzymuje odpowiedzi hello pytania toohello niewłaściwy, procesu wyboru hello będzie się powtarzał atakowaniu pytanie tooprevent.</span><span class="sxs-lookup"><span data-stu-id="1f349-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="1f349-177">**Pytanie: czy można uniemożliwić użytkownikom próby resetowania wielokrotnie w krótkim przedziale czasu?**</span><span class="sxs-lookup"><span data-stu-id="1f349-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="1f349-178">**Odpowiedź:** tak, są wbudowane w tooprotect resetowania hasła przed niewłaściwym użyciem funkcje zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1f349-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="1f349-179">Użytkownicy mogą tylko spróbuj 5 próbach resetowania hasła w ciągu godziny przed jest zablokowane przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="1f349-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="1f349-180">Użytkownicy mogą tylko spróbuj toovalidate numeru telefonu, 5 razy w ciągu godziny przed jest zablokowane przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="1f349-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="1f349-181">Użytkownicy mogą tylko spróbuj użyć metody pojedynczego uwierzytelniania 5 razy w ciągu godziny przed jest zablokowane przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="1f349-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="1f349-182">**Pytanie: na jak długo są prawidłowe hello poczty e-mail i SMS jednorazowy kod dostępu?**</span><span class="sxs-lookup"><span data-stu-id="1f349-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="1f349-183">**Odpowiedź:** hello okres istnienia sesji do resetowania hasła jest 105 minut.</span><span class="sxs-lookup"><span data-stu-id="1f349-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="1f349-184">Od początku hello hello operacji resetowania hasła, hello użytkownika tooreset 105 minut swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="1f349-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="1f349-185">Witaj poczty e-mail i SMS jednorazowy kod dostępu są nieprawidłowe po tym okresie.</span><span class="sxs-lookup"><span data-stu-id="1f349-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="1f349-186">Zmienianie hasła</span><span class="sxs-lookup"><span data-stu-id="1f349-186">Password change</span></span>
* <span data-ttu-id="1f349-187">**Pytanie: gdzie powinien Moi użytkownicy? toochange haseł**</span><span class="sxs-lookup"><span data-stu-id="1f349-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="1f349-188">**A:** użytkownicy mogą zmieniać swoje hasła dowolnym Zobacz ich obraz profilu lub ikonę (podobnie jak w hello prawym górnym rogu ich [usługi Office 365](https://portal.office.com) lub [panelu dostępu](https://myapps.microsoft.com) wykonywania.</span><span class="sxs-lookup"><span data-stu-id="1f349-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="1f349-189">Użytkownicy mogą zmieniać swoje hasła z hello [strony panelu dostępu profilu](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="1f349-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="1f349-190">Użytkownicy mogą również być zadawane toochange haseł automatycznie ekranu logowania hello Azure AD, jeśli ich hasła wygasły.</span><span class="sxs-lookup"><span data-stu-id="1f349-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="1f349-191">Ponadto użytkownicy mogą przechodzić toohello [Portal zmiany hasła programu Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) bezpośrednio próbujące toochange haseł.</span><span class="sxs-lookup"><span data-stu-id="1f349-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="1f349-192">**Pytanie: czy Moi użytkownicy powiadamianych w portalu usługi Office hello po wygaśnięciu hasła lokalnego?**</span><span class="sxs-lookup"><span data-stu-id="1f349-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="1f349-193">**Odpowiedź:** jest to możliwe dzisiaj Jeśli używasz usług AD FS, wykonując instrukcje hello tutaj: [wysyłanie oświadczeń zasad haseł z usług AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="1f349-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="1f349-194">Jeśli używasz synchronizacji skrótu hasła nie jest to możliwe dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="1f349-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="1f349-195">Jest to spowodowane nie zsynchronizować zasad haseł z lokalnej, więc nie jest możliwe w firmie Microsoft napotyka toopost wygaśnięcia powiadomienia toocloud.</span><span class="sxs-lookup"><span data-stu-id="1f349-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="1f349-196">W obu przypadkach możliwe jest również zbyt[Powiadom użytkowników, których hasła są o tooexpire przy użyciu programu PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f349-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="1f349-197">Raporty zarządzania hasła</span><span class="sxs-lookup"><span data-stu-id="1f349-197">Password management reports</span></span>
* <span data-ttu-id="1f349-198">**Pytanie: jak długo trwa dla danych tooshow się na raporty zarządzania hello hasło?**</span><span class="sxs-lookup"><span data-stu-id="1f349-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="1f349-199">**Odpowiedź:** danych powinny pojawiać się na raporty zarządzania hello hasła w ciągu 5 – 10 minut.</span><span class="sxs-lookup"><span data-stu-id="1f349-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="1f349-200">Go niektórych wystąpień może trwać tooan tooappear godzinę.</span><span class="sxs-lookup"><span data-stu-id="1f349-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="1f349-201">**Pytanie: jak można filtrować raporty zarządzania hello hasło?**</span><span class="sxs-lookup"><span data-stu-id="1f349-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="1f349-202">**Odpowiedź:** można filtrować raporty zarządzania hello hasło, klikając hello małych Lupa toohello extreme prawej hello etykiety kolumn, górze hello hello raportu.</span><span class="sxs-lookup"><span data-stu-id="1f349-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="1f349-203">Jeśli chcesz bardziej zaawansowane funkcje filtrowania toodo, można pobrać hello tooexcel raportu i utworzyć tabelę przestawną.</span><span class="sxs-lookup"><span data-stu-id="1f349-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="1f349-204">**Pytanie: jaka jest maksymalna liczba zdarzeń hello są przechowywane w raportach zarządzania hasło hello?**</span><span class="sxs-lookup"><span data-stu-id="1f349-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="1f349-205">**Odpowiedź:** się too75, 000 hasła resetowania lub hasło resetowania rejestracji zdarzenia są przechowywane w raporty zarządzania hasło hello spanning Utwórz kopię zapasową too30 dni.</span><span class="sxs-lookup"><span data-stu-id="1f349-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="1f349-206">Pracujemy nad tym tooexpand to numer tooinclude więcej zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1f349-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="1f349-207">**Pytanie: jak daleko raporty zarządzania hasło hello go?**</span><span class="sxs-lookup"><span data-stu-id="1f349-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="1f349-208">**Odpowiedź:** zarządzania hasłami hello raporty operacji Pokaż występujących hello ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="1f349-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="1f349-209">Teraz Jeśli potrzebujesz tooarchive te dane, można pobrać raporty hello okresowo i zapisać je w innej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="1f349-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="1f349-210">**Pytanie: istnieje już maksymalną liczbę wierszy, które mogą być wyświetlane w raportach zarządzania hasło hello?**</span><span class="sxs-lookup"><span data-stu-id="1f349-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="1f349-211">**Odpowiedź:** tak, maksymalnie 75,000 wierszy może pojawić się w zależności od hello raporty zarządzania hasło, czy są one wyświetlane w hello interfejsu użytkownika lub pobierania.</span><span class="sxs-lookup"><span data-stu-id="1f349-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="1f349-212">**Pytanie: istnieje już tooaccess interfejsu API hello hasła resetowania lub rejestracji raportowania danych?**</span><span class="sxs-lookup"><span data-stu-id="1f349-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="1f349-213">**Odpowiedź:** tak, zobacz powitania po dokumentacji toolearn uzyskać dostęp hasła hello zresetować strumienia danych raportowania.</span><span class="sxs-lookup"><span data-stu-id="1f349-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="1f349-214">[Dowiedz się, jak tooaccess resetowania hasła zdarzeń do raportowania programowo](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="1f349-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="1f349-215">Zapisywanie zwrotne haseł</span><span class="sxs-lookup"><span data-stu-id="1f349-215">Password writeback</span></span>
* <span data-ttu-id="1f349-216">**Pytanie: jak działa funkcji zapisywania zwrotnego haseł w tle hello?**</span><span class="sxs-lookup"><span data-stu-id="1f349-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="1f349-217">**Odpowiedź:** zobacz [sposób działania funkcji zapisywania zwrotnego haseł](active-directory-passwords-writeback.md) dla wyjaśnienie, co się stanie po włączeniu funkcji zapisywania zwrotnego haseł i jak dane przepływają przez hello system wrócić do środowiska lokalnego.</span><span class="sxs-lookup"><span data-stu-id="1f349-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="1f349-218">**Pytanie: jak długo funkcji zapisywania zwrotnego haseł trwa toowork?  Czy istnieje opóźnienie synchronizacji jak z synchronizacji skrótów haseł?**</span><span class="sxs-lookup"><span data-stu-id="1f349-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="1f349-219">**Odpowiedź:** błyskawicznych jest funkcji zapisywania zwrotnego haseł.</span><span class="sxs-lookup"><span data-stu-id="1f349-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="1f349-220">Jest synchroniczne potok, który działa zasadniczo inaczej niż synchronizacji skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="1f349-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="1f349-221">Zapisywanie zwrotne haseł umożliwia użytkownikom tooget w czasie rzeczywistym swoją opinię na temat powodzenia hello hasła Resetowanie lub zmienianie operacji.</span><span class="sxs-lookup"><span data-stu-id="1f349-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="1f349-222">Średni czas pomyślnego funkcji zapisywania zwrotnego haseł Hello jest w obszarze 500 ms.</span><span class="sxs-lookup"><span data-stu-id="1f349-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="1f349-223">**Pytanie: Jeśli konto lokalne jest wyłączone, Moje konto/dostęp do chmury wpływ?**</span><span class="sxs-lookup"><span data-stu-id="1f349-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="1f349-224">**Odpowiedź:** wyłączenie Identyfikatora lokalnej chmury również zostaną wyłączone identyfikator/access interwałem hello następnej synchronizacji za pomocą domyślnego byt AAD Connect to co 30 minut.</span><span class="sxs-lookup"><span data-stu-id="1f349-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="1f349-225">**Pytanie: czy Moje konto lokalne jest ograniczane przez zasady haseł lokalnej usługi Active Directory, SSPR przestrzegać tych zasad po zmianie hasła hello?**</span><span class="sxs-lookup"><span data-stu-id="1f349-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="1f349-226">**Odpowiedź:** tak, zależy od usługi SSPR i przestrzega zasad hello lokalne zasady haseł AD, w tym typowych zasad haseł domeny AD, a także wszystkie zdefiniowane zasady haseł szczegółowe docelowe tooa danego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1f349-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="1f349-227">**Pytanie: jakie typy kont zapisywania zwrotnego haseł działa dla?**</span><span class="sxs-lookup"><span data-stu-id="1f349-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="1f349-228">**Odpowiedź:** funkcji zapisywania zwrotnego haseł działa w przypadku federacyjnym i synchronizacji skrótów haseł użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1f349-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="1f349-229">**Pytanie: czy funkcji zapisywania zwrotnego haseł wymusić zasady haseł mojej domeny?**</span><span class="sxs-lookup"><span data-stu-id="1f349-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="1f349-230">**Odpowiedź:** tak, funkcję zapisywania zwrotnego haseł wymusza okres ważności hasła, historii złożoności, filtrów i inne ograniczenia, może umieścić w miejscu na haseł w domenie lokalnej.</span><span class="sxs-lookup"><span data-stu-id="1f349-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="1f349-231">**Pytanie: czy jest bezpieczna funkcji zapisywania zwrotnego haseł?  Jak można mieć pewność, że I nie będzie włamania?**</span><span class="sxs-lookup"><span data-stu-id="1f349-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="1f349-232">**Odpowiedź:** tak, zapisywanie zwrotne haseł jest bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="1f349-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="1f349-233">tooread więcej informacji na temat hello cztery warstwy zabezpieczeń zaimplementowana przez usługę zapisywania zwrotnego haseł hello, zapoznaj się z hello [model zabezpieczeń zapisywania zwrotnego haseł](active-directory-passwords-writeback.md#password-writeback-security-model) sekcji w sposób działania funkcji zapisywania zwrotnego haseł.</span><span class="sxs-lookup"><span data-stu-id="1f349-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="1f349-234">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f349-234">Next steps</span></span>

<span data-ttu-id="1f349-235">Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f349-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="1f349-236">[**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f349-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="1f349-237">[**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f349-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="1f349-238">[**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami</span><span class="sxs-lookup"><span data-stu-id="1f349-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="1f349-239">[**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj</span><span class="sxs-lookup"><span data-stu-id="1f349-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="1f349-240">[**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.</span><span class="sxs-lookup"><span data-stu-id="1f349-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="1f349-241">[**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="1f349-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="1f349-242">[**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie</span><span class="sxs-lookup"><span data-stu-id="1f349-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="1f349-243">[**Zapisywanie zwrotne haseł**](active-directory-passwords-writeback.md) — Jak zapisywanie zwrotne haseł współpracuje z katalogiem lokalnym</span><span class="sxs-lookup"><span data-stu-id="1f349-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="1f349-244">[**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa</span><span class="sxs-lookup"><span data-stu-id="1f349-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="1f349-245">[**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR</span><span class="sxs-lookup"><span data-stu-id="1f349-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
