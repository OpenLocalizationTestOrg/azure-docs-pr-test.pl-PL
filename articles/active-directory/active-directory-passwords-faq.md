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
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="0ce46-104">Często zadawane pytania dotyczące zarządzania hasłami</span><span class="sxs-lookup"><span data-stu-id="0ce46-104">Password management frequently asked questions</span></span>

<span data-ttu-id="0ce46-105">Poniżej przedstawiono niektóre często zadawane pytania dla wszystkich czynności związane z resetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="0ce46-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="0ce46-106">Jeśli masz pytania ogólne dotyczące usługi Azure AD i hasło samoobsługowego resetowania, który nie ma odpowiedzi w tym miejscu, można zadawać społeczności pomocy na [fora usługi Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="0ce46-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="0ce46-107">Członkowie społeczności obejmują Engineers, menedżerów produktu MVP i twarzy specjalistów IT.</span><span class="sxs-lookup"><span data-stu-id="0ce46-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="0ce46-108">Często zadawane pytania jest podzielony na następujące sekcje:</span><span class="sxs-lookup"><span data-stu-id="0ce46-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="0ce46-109">**Pytania dotyczące rejestracji resetowania hasła**</span><span class="sxs-lookup"><span data-stu-id="0ce46-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="0ce46-110">**Pytania dotyczące resetowania hasła**</span><span class="sxs-lookup"><span data-stu-id="0ce46-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="0ce46-111">**Pytania dotyczące zmiany hasła**</span><span class="sxs-lookup"><span data-stu-id="0ce46-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="0ce46-112">**Raporty pytania dotyczące zarządzania hasłami**</span><span class="sxs-lookup"><span data-stu-id="0ce46-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="0ce46-113">**Pytania dotyczące funkcji zapisywania zwrotnego haseł**</span><span class="sxs-lookup"><span data-stu-id="0ce46-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="0ce46-114">Rejestracja resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="0ce46-114">Password reset registration</span></span>
* <span data-ttu-id="0ce46-115">**Pytanie: czy Moi użytkownicy rejestrowanie własnych danych resetowania hasła?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="0ce46-116">**Odpowiedź:** tak, jak długo resetowania hasła jest włączona i są one licencjonowane, może przejść do portalu rejestracji resetowania haseł pod adresem http://aka.ms/ssprsetup zarejestrować swoje informacje o uwierzytelnianiu.</span><span class="sxs-lookup"><span data-stu-id="0ce46-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="0ce46-117">Użytkownicy mogą również zarejestrować, przechodząc do panelu dostępu pod adresem http://myapps.microsoft.com, klikając kartę profilu i klikając rejestru dla opcji resetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="0ce46-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="0ce46-118">**Q: czy można zdefiniować dane resetowania hasła w imieniu użytkowników?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="0ce46-119">**Odpowiedź:** tak, możesz to zrobić z programem Azure AD Connect, programu PowerShell, [portalu Azure](https://portal.azure.com), lub w portalu administracyjnym pakietu Office.</span><span class="sxs-lookup"><span data-stu-id="0ce46-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="0ce46-120">Aby uzyskać więcej informacji, zobacz artykuł [dane używane przez usługi Azure AD samoobsługowego resetowania hasła](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="0ce46-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="0ce46-121">**Pytanie: czy można synchronizować dane odpowiedzi na pytania zabezpieczające z lokalnie?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="0ce46-122">**Odpowiedź:** nie jest to możliwe dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="0ce46-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="0ce46-123">**Pytanie: czy Moi użytkownicy zarejestrować danych w taki sposób, że inni użytkownicy nie widzą te dane?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="0ce46-124">**Odpowiedź:** tak, gdy użytkownicy rejestrują danych przy użyciu portalu resetowania haseł rejestracji jest zapisywany do pól prywatnych uwierzytelniania, które są tylko widoczne, Administratorzy globalni i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ce46-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="0ce46-125">Jeśli **konto administratora platformy Azure** rejestruje numer telefonu uwierzytelniania również są umieszczane w polu telefonu komórkowego i jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="0ce46-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="0ce46-126">**Pytanie: czy Moi użytkownicy muszą być zarejestrowane, aby móc korzystać z resetowania hasła?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="0ce46-127">**Odpowiedź:** nie, w przypadku definiowania wystarczających informacji uwierzytelniania w ich imieniu, użytkownicy muszą zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="0ce46-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="0ce46-128">Działania resetowania hasła, tak długo, jak długo ma prawidłowo sformatowane dane przechowywane w odpowiednich polach w katalogu.</span><span class="sxs-lookup"><span data-stu-id="0ce46-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="0ce46-129">**Pytanie: można zsynchronizować lub ustawić adres E-mail uwierzytelniania lub alternatywny numer telefonu uwierzytelniania pól, numer telefonu uwierzytelniania w imieniu użytkowników?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="0ce46-130">**Odpowiedź:** nie jest to możliwe dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="0ce46-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="0ce46-131">**Pytanie: jak portal rejestracji wiedzieć jakie opcje Pokaż moich użytkowników?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="0ce46-132">**Odpowiedź:** portalu rejestracji resetowania haseł wyświetlane są tylko opcje włączeniu dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0ce46-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="0ce46-133">Te opcje można znaleźć w sekcji zasady resetowania hasła użytkownika, karta Konfigurowanie w katalogu.</span><span class="sxs-lookup"><span data-stu-id="0ce46-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="0ce46-134">Na przykład oznacza to, że jeśli pytania zabezpieczające nie jest włączona, następnie użytkownicy nie mają możliwości rejestrowania dla tej opcji.</span><span class="sxs-lookup"><span data-stu-id="0ce46-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="0ce46-135">**Pytanie: Jeśli użytkownik jest uznawany zarejestrowane?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="0ce46-136">**A:** użytkownik jest uznawany w zarejestrowany dla usługi SSPR, gdy zarejestrowanych co najmniej **wiele metod wymaganych do zresetowania** ustawioną [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ce46-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="0ce46-137">Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="0ce46-137">Password reset</span></span>
* <span data-ttu-id="0ce46-138">**Pytanie: jak długo należy czekać do odbierania wiadomości e-mail, SMS lub połączeń telefonicznych z resetowania hasła?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="0ce46-139">**Odpowiedź:** poczty E-mail, wiadomości SMS i połączeń telefonicznych powinna odbierane w obszarze jedną minutę, z normalna sytuacja 5-20 sekund.</span><span class="sxs-lookup"><span data-stu-id="0ce46-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="0ce46-140">Jeśli użytkownik nie otrzyma powiadomienie w tym czasie:</span><span class="sxs-lookup"><span data-stu-id="0ce46-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="0ce46-141">Sprawdź folder wiadomości-śmieci.</span><span class="sxs-lookup"><span data-stu-id="0ce46-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="0ce46-142">Czy numer lub adres e-mail jest nawiązywane połączenie jest oczekiwane.</span><span class="sxs-lookup"><span data-stu-id="0ce46-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="0ce46-143">Sprawdź, czy dane uwierzytelniania w katalogu jest poprawnie sformatowana.</span><span class="sxs-lookup"><span data-stu-id="0ce46-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="0ce46-144">Przykład: "+ 1 4255551234" lub "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="0ce46-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="0ce46-145">**Pytanie: jakie języki są obsługiwane przez resetowania hasła?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="0ce46-146">**Odpowiedź:** resetowania hasła użytkownika wiadomości SMS i połączeń głosowych są zlokalizowane w te same języki, które są obsługiwane w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="0ce46-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="0ce46-147">**Karta na konfigurowanie Q: części środowisko resetowania hasła uzyskać marki, gdy ustawić organizacji znakowania w katalogu Moje?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="0ce46-148">**Odpowiedź:** portal resetowania haseł pokazuje logo organizacji i pozwala na skonfigurowanie kontaktu link do administratora wskazywał niestandardowe wiadomości e-mail lub adres URL.</span><span class="sxs-lookup"><span data-stu-id="0ce46-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="0ce46-149">Każdej wiadomości e-mail, które są wysyłane przez resetowania haseł obejmuje logo organizacji, kolory, nazwy w treści wiadomości e-mail i dostosować na podstawie nazwy.</span><span class="sxs-lookup"><span data-stu-id="0ce46-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="0ce46-150">**Pytanie: jak można Poinformuj użytkowników o tym, gdzie można przejść na resetowanie haseł?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="0ce46-151">**A:** użytkowników można wysyłać bezpośrednio do https://passwordreset.microsoftonline.com lub polecić, kliknięcie **nie ma dostępu do konta łącze** na dowolnej pracy lub nauki strony logowania.</span><span class="sxs-lookup"><span data-stu-id="0ce46-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="0ce46-152">Można również opublikować te linki w miejscu łatwo dostępne dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0ce46-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="0ce46-153">**Pytanie: czy można użyć tej strony z urządzenia przenośnego?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="0ce46-154">**Odpowiedź:** tak, ta strona działa na urządzeniach przenośnych.</span><span class="sxs-lookup"><span data-stu-id="0ce46-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="0ce46-155">**Pytanie: czy odblokowywanie kont z lokalnej usługi active directory są obsługiwane podczas użytkownikom resetowania swoich haseł w?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="0ce46-156">**Odpowiedź:** tak, gdy użytkownik resetuje hasła i zapisywania zwrotnego haseł został wdrożony za pomocą usługi Azure AD Connect, konto użytkownika jest odblokowany automatycznie podczas resetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="0ce46-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="0ce46-157">**Pytanie: jak można zintegrować resetowania bezpośrednio do mojego użytkownika logowania środowisko pulpitu**</span><span class="sxs-lookup"><span data-stu-id="0ce46-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="0ce46-158">**Odpowiedź:** w przypadku klienta programu Azure AD Premium można zainstalować programu Microsoft Identity Manager bez ponoszenia dodatkowych kosztów i wdrażania rozwiązania resetowania hasła lokalnego, aby spełnić to wymaganie.</span><span class="sxs-lookup"><span data-stu-id="0ce46-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="0ce46-159">**Pytanie: czy można ustawić pytania zabezpieczeń dla różnych ustawień regionalnych?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="0ce46-160">**Odpowiedź:** nie jest to możliwe dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="0ce46-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="0ce46-161">**Pytanie: jak wiele pytań możemy skonfigurować dla opcji uwierzytelniania pytania zabezpieczające?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="0ce46-162">**Odpowiedź:** można skonfigurować maksymalnie 20 pytania zabezpieczające niestandardowych w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ce46-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="0ce46-163">**Pytanie: jak długo może być pytania zabezpieczające?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="0ce46-164">**Odpowiedź:** pytania zabezpieczające może mieć długość od 3 do 200 znaków.</span><span class="sxs-lookup"><span data-stu-id="0ce46-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="0ce46-165">**Pytanie: jak długo może być odpowiedzi na pytania zabezpieczające?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="0ce46-166">**Odpowiedź:** odpowiedzi może być 3 do 40 znaków.</span><span class="sxs-lookup"><span data-stu-id="0ce46-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="0ce46-167">**Pytanie: czy zduplikowane odpowiedzi na pytania zabezpieczające odrzucone?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="0ce46-168">**Odpowiedź:** tak, możemy Odrzuć zduplikowane odpowiedzi na pytania zabezpieczające.</span><span class="sxs-lookup"><span data-stu-id="0ce46-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="0ce46-169">**Pytanie: czy maja użytkownika zarejestrować na tym samym pytanie zabezpieczające więcej niż raz?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="0ce46-170">**Odpowiedź:** nie, gdy użytkownik rejestruje dane pytanie, ich nie może zarejestrować dla tego zapytania po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="0ce46-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="0ce46-171">**Pytanie: czy jest możliwe ustawić minimalny limit pytania zabezpieczające dla rejestracji i zresetować?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="0ce46-172">**Odpowiedź:** tak, można ustawić limit jeden dla rejestracji i drugi dla resetowania.</span><span class="sxs-lookup"><span data-stu-id="0ce46-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="0ce46-173">pytania zabezpieczające 3 – 5 może być wymagany w czasie rejestracji i 3 – 5 mogą być wymagane w celu resetowania.</span><span class="sxs-lookup"><span data-stu-id="0ce46-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="0ce46-174">**Pytanie: Jeśli użytkownik został zarejestrowany w więcej niż maksymalna liczba pytań wymaganych do zresetowania, jak są pytania zabezpieczające wybrane podczas resetowania?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="0ce46-175">**Odpowiedź:** N pytania zabezpieczające są losowo wybrane poza łączna liczba pytań, użytkownik został zarejestrowany, gdzie N to **liczby pytań wymaganych do zresetowania**.</span><span class="sxs-lookup"><span data-stu-id="0ce46-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="0ce46-176">Na przykład jeśli użytkownik ma 5 pytania zabezpieczające w zarejestrowany, ale do resetowania wymagane są tylko 3, 3, 5 są wybierane losowo i przedstawionego na resetowanie.</span><span class="sxs-lookup"><span data-stu-id="0ce46-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="0ce46-177">Jeśli użytkownik pobiera nieprawidłowe odpowiedzi na pytania, aby zapobiec atakowaniu pytanie będzie się powtarzał procesu wyboru.</span><span class="sxs-lookup"><span data-stu-id="0ce46-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="0ce46-178">**Pytanie: czy można uniemożliwić użytkownikom próby resetowania wielokrotnie w krótkim przedziale czasu?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="0ce46-179">**Odpowiedź:** tak, są wbudowane w resetowania hasła, aby chronić przed niewłaściwym użyciem funkcje zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="0ce46-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="0ce46-180">Użytkownicy mogą tylko spróbuj 5 próbach resetowania hasła w ciągu godziny przed jest zablokowane przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="0ce46-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="0ce46-181">Użytkownicy mogą tylko spróbuj można sprawdzić poprawności numeru telefonu 5 razy w ciągu godziny przed jest zablokowane przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="0ce46-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="0ce46-182">Użytkownicy mogą tylko spróbuj użyć metody pojedynczego uwierzytelniania 5 razy w ciągu godziny przed jest zablokowane przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="0ce46-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="0ce46-183">**Pytanie: na jak długo są prawidłowe poczty e-mail i SMS jednorazowy kod dostępu?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="0ce46-184">**Odpowiedź:** okres istnienia sesji do resetowania hasła jest 105 minut.</span><span class="sxs-lookup"><span data-stu-id="0ce46-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="0ce46-185">Od początku operacji resetowania hasła użytkownika ma 105 minut, aby zresetować swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="0ce46-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="0ce46-186">Po tym okresie poczty e-mail i SMS jednorazowy kod dostępu są nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="0ce46-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="0ce46-187">Zmienianie hasła</span><span class="sxs-lookup"><span data-stu-id="0ce46-187">Password change</span></span>
* <span data-ttu-id="0ce46-188">**Pytanie: gdzie Moi użytkownicy powinien przejść do zmiany haseł?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="0ce46-189">**A:** użytkownicy mogą zmieniać swoje hasła dowolnym Zobacz ich obraz profilu lub ikonę (w prawym górnym rogu, takich jak ich [usługi Office 365](https://portal.office.com) lub [panelu dostępu](https://myapps.microsoft.com) wykonywania.</span><span class="sxs-lookup"><span data-stu-id="0ce46-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="0ce46-190">Użytkownicy mogą zmieniać swoje hasła z [strony panelu dostępu profilu](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="0ce46-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="0ce46-191">Użytkownicy mogą również poproszony o zmiany haseł automatycznie ekranu logowania usługi Azure AD, jeśli ich hasła wygasły.</span><span class="sxs-lookup"><span data-stu-id="0ce46-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="0ce46-192">Ponadto użytkownicy mogą przechodzić do [Portal zmiany hasła programu Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) bezpośrednio Jeśli chcesz zmienić swoje hasła.</span><span class="sxs-lookup"><span data-stu-id="0ce46-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="0ce46-193">**Pytanie: czy Moi użytkownicy powiadamianych w portalu usługi Office po wygaśnięciu hasła lokalnego?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="0ce46-194">**Odpowiedź:** jest to możliwe dzisiaj Jeśli używasz usług AD FS, postępując zgodnie z instrukcjami w tym miejscu: [wysyłanie oświadczeń zasad haseł z usług AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="0ce46-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="0ce46-195">Jeśli używasz synchronizacji skrótu hasła nie jest to możliwe dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="0ce46-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="0ce46-196">Jest to spowodowane nie zsynchronizować zasad haseł z lokalnej, więc nie jest możliwe w firmie Microsoft można wysłać powiadomienia o wygasaniu do środowiska chmury.</span><span class="sxs-lookup"><span data-stu-id="0ce46-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="0ce46-197">W obu przypadkach istnieje również możliwość [Powiadom użytkowników, których hasła zbliża się termin wygaśnięcia przy użyciu programu PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ce46-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="0ce46-198">Raporty zarządzania hasła</span><span class="sxs-lookup"><span data-stu-id="0ce46-198">Password management reports</span></span>
* <span data-ttu-id="0ce46-199">**Pytanie: jak długo trwa danych wyświetlani w raportach zarządzania hasło?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="0ce46-200">**Odpowiedź:** danych powinny pojawiać się na raporty zarządzania hasła w ciągu 5 – 10 minut.</span><span class="sxs-lookup"><span data-stu-id="0ce46-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="0ce46-201">Go niektórych wystąpień może potrwać do godziny pojawią się.</span><span class="sxs-lookup"><span data-stu-id="0ce46-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="0ce46-202">**Pytanie: jak można filtrować raporty zarządzania hasło?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="0ce46-203">**Odpowiedź:** można filtrować raporty zarządzania hasło, klikając małych Lupa extreme po prawej stronie etykiety kolumn, w górnej części raportu.</span><span class="sxs-lookup"><span data-stu-id="0ce46-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="0ce46-204">Jeśli chcesz bardziej rozbudowane filtrowanie, można pobrać raportu i utworzyć tabelę przestawną w programie excel.</span><span class="sxs-lookup"><span data-stu-id="0ce46-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="0ce46-205">**Pytanie: jaka jest maksymalna liczba zdarzeń są przechowywane w raportach dotyczących zarządzania hasło?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="0ce46-206">**Odpowiedź:** maksymalnie 75,000 resetowania lub hasło rejestracji resetowania hasła zdarzenia są przechowywane w raportach dotyczących zarządzania hasła, obejmujących kopii maksymalnie 30 dni.</span><span class="sxs-lookup"><span data-stu-id="0ce46-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="0ce46-207">Pracujemy nad Rozwiń ten numer, aby zarejestrować więcej zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="0ce46-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="0ce46-208">**Pytanie: jak daleko raporty zarządzania hasło go?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="0ce46-209">**Odpowiedź:** zarządzania hasłami raporty operacji Pokaż wykonywanych w ciągu ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="0ce46-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="0ce46-210">Teraz Jeśli chcesz zarchiwizować te dane, musisz można pobrać raporty okresowo i zapisać je w innej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0ce46-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="0ce46-211">**Pytanie: istnieje już maksymalną liczbę wierszy, które mogą być wyświetlane w raportach zarządzania hasło?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="0ce46-212">**Odpowiedź:** tak, maksymalnie 75,000 wierszy może pojawić się w zależności od raporty zarządzania hasło, czy są są wyświetlane w interfejsie użytkownika lub pobierania.</span><span class="sxs-lookup"><span data-stu-id="0ce46-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="0ce46-213">**Pytanie: jest interfejs API dostępu do resetowania hasła lub rejestracji dane raportowania?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="0ce46-214">**Odpowiedź:** tak, zobacz następującą dokumentację, aby dowiedzieć się, jak można pobrać resetowania hasła, strumień danych raportowania.</span><span class="sxs-lookup"><span data-stu-id="0ce46-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="0ce46-215">[Dowiedz się, jak uzyskać dostępu do zdarzeń do raportowania programowane Resetowanie hasła](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="0ce46-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="0ce46-216">Zapisywanie zwrotne haseł</span><span class="sxs-lookup"><span data-stu-id="0ce46-216">Password writeback</span></span>
* <span data-ttu-id="0ce46-217">**Pytanie: jak działa funkcji zapisywania zwrotnego haseł w tle?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="0ce46-218">**Odpowiedź:** zobacz [sposób działania funkcji zapisywania zwrotnego haseł](active-directory-passwords-writeback.md) dla wyjaśnienie, co się stanie po włączeniu funkcji zapisywania zwrotnego haseł i sposób dane przepływają przez system do środowiska lokalnego.</span><span class="sxs-lookup"><span data-stu-id="0ce46-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="0ce46-219">**Pytanie: jak długo funkcji zapisywania zwrotnego haseł podąża pracę?  Czy istnieje opóźnienie synchronizacji jak z synchronizacji skrótów haseł?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="0ce46-220">**Odpowiedź:** błyskawicznych jest funkcji zapisywania zwrotnego haseł.</span><span class="sxs-lookup"><span data-stu-id="0ce46-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="0ce46-221">Jest synchroniczne potok, który działa zasadniczo inaczej niż synchronizacji skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="0ce46-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="0ce46-222">Zapisywanie zwrotne haseł umożliwia użytkownikom Uzyskaj opinie w czasie rzeczywistym o udanym ich resetowania hasła lub zmienić operację.</span><span class="sxs-lookup"><span data-stu-id="0ce46-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="0ce46-223">Średni czas na pomyślne zapisywania zwrotnego hasła jest w obszarze 500 ms.</span><span class="sxs-lookup"><span data-stu-id="0ce46-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="0ce46-224">**Pytanie: Jeśli konto lokalne jest wyłączone, Moje konto/dostęp do chmury wpływ?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="0ce46-225">**Odpowiedź:** wyłączenie Identyfikatora lokalnej chmury identyfikator/access również zostaną wyłączone w następnym interwale czasowym synchronizacji za pomocą domyślnego byt AAD Connect to co 30 minut.</span><span class="sxs-lookup"><span data-stu-id="0ce46-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="0ce46-226">**Pytanie: czy Moje konto lokalne jest ograniczane przez zasady haseł lokalnej usługi Active Directory, SSPR przestrzegać tych zasad po zmianie hasła?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="0ce46-227">**Odpowiedź:** tak, SSPR opiera się na i przestrzega zasad lokalnych zasad haseł usługi AD, w tym typowych zasad haseł domeny usługi AD, a także wszelkie zdefiniowane zasady szczegółowe hasło przeznaczone dla danego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ce46-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="0ce46-228">**Pytanie: jakie typy kont zapisywania zwrotnego haseł działa dla?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="0ce46-229">**Odpowiedź:** funkcji zapisywania zwrotnego haseł działa w przypadku federacyjnym i synchronizacji skrótów haseł użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0ce46-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="0ce46-230">**Pytanie: czy funkcji zapisywania zwrotnego haseł wymusić zasady haseł mojej domeny?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="0ce46-231">**Odpowiedź:** tak, funkcję zapisywania zwrotnego haseł wymusza okres ważności hasła, historii złożoności, filtrów i inne ograniczenia, może umieścić w miejscu na haseł w domenie lokalnej.</span><span class="sxs-lookup"><span data-stu-id="0ce46-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="0ce46-232">**Pytanie: czy jest bezpieczna funkcji zapisywania zwrotnego haseł?  Jak można mieć pewność, że I nie będzie włamania?**</span><span class="sxs-lookup"><span data-stu-id="0ce46-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="0ce46-233">**Odpowiedź:** tak, zapisywanie zwrotne haseł jest bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="0ce46-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="0ce46-234">Aby uzyskać więcej informacji na temat cztery warstwy zabezpieczeń zaimplementowanych przez usługę zapisywania zwrotnego haseł, zapoznaj się [model zabezpieczeń zapisywania zwrotnego haseł](active-directory-passwords-writeback.md#password-writeback-security-model) sekcji w sposób działania funkcji zapisywania zwrotnego haseł.</span><span class="sxs-lookup"><span data-stu-id="0ce46-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="0ce46-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ce46-235">Next steps</span></span>

<span data-ttu-id="0ce46-236">Poniższe linki dają dostęp do dodatkowych informacji dotyczących resetowania haseł za pomocą usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ce46-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="0ce46-237">[**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ce46-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="0ce46-238">[**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ce46-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="0ce46-239">[**Dane**](active-directory-passwords-data.md) — Omówienie wymaganych danych i sposobu ich wykorzystania w zarządzaniu hasłami</span><span class="sxs-lookup"><span data-stu-id="0ce46-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="0ce46-240">[**Wdrażanie**](active-directory-passwords-best-practices.md) — Planowanie funkcji samoobsługowego resetowania haseł i jej wdrażanie dla użytkowników przy użyciu znajdujących się tu wytycznych</span><span class="sxs-lookup"><span data-stu-id="0ce46-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="0ce46-241">[**Dostosowywanie**](active-directory-passwords-customize.md) — Dostosowywanie wyglądu i działania środowiska samoobsługowego resetowania haseł dla firmy</span><span class="sxs-lookup"><span data-stu-id="0ce46-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="0ce46-242">[**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="0ce46-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="0ce46-243">[**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie</span><span class="sxs-lookup"><span data-stu-id="0ce46-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="0ce46-244">[**Zapisywanie zwrotne haseł**](active-directory-passwords-writeback.md) — Jak zapisywanie zwrotne haseł współpracuje z katalogiem lokalnym</span><span class="sxs-lookup"><span data-stu-id="0ce46-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="0ce46-245">[**Szczegóły techniczne**](active-directory-passwords-how-it-works.md) — Informacje o tym, co dzieje się za kulisami tej funkcji i jak ona działa</span><span class="sxs-lookup"><span data-stu-id="0ce46-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="0ce46-246">[**Rozwiązywanie problemów**](active-directory-passwords-troubleshoot.md) — Informacje o tym, jak rozwiązywać typowe problemy z samoobsługowym resetowaniem haseł</span><span class="sxs-lookup"><span data-stu-id="0ce46-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
