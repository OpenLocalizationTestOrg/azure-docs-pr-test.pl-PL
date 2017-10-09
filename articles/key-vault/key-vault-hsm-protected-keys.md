---
title: "aaaHow toogenerate i przeniesienia chronionego przez moduł HSM kluczy dla usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Użyj tego toohelp artykule planowanie, generowanie i przekazać swoje własne klucze chronione przez moduł HSM toouse z usługi Azure Key Vault. Znany również jako BYOK lub własnego klucza."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="d28ca-104">Jak toogenerate i przenoszenie kluczy chronionych HSM dla usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d28ca-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="d28ca-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="d28ca-105">Introduction</span></span>
<span data-ttu-id="d28ca-106">Dla dodatkowego bezpieczeństwa korzystając z usługi Azure Key Vault, można zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM hello.</span><span class="sxs-lookup"><span data-stu-id="d28ca-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="d28ca-107">Ten scenariusz jest często określonego tooas *własnego klucza*, byok.</span><span class="sxs-lookup"><span data-stu-id="d28ca-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="d28ca-108">Witaj sprzętowych modułów zabezpieczeń są FIPS 140-2 poziom 2 zweryfikowany.</span><span class="sxs-lookup"><span data-stu-id="d28ca-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="d28ca-109">Usługa Azure Key Vault używa rodziny nShield firmy Thales tooprotect sprzętowych modułów zabezpieczeń z kluczy.</span><span class="sxs-lookup"><span data-stu-id="d28ca-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="d28ca-110">Użyj informacji hello w tym toohelp temacie Planowanie, generowanie i przekazać swoje własne klucze chronione przez moduł HSM toouse z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d28ca-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="d28ca-111">Ta funkcja nie jest dostępna dla Chińskiej wersji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d28ca-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="d28ca-112">Aby uzyskać więcej informacji na temat usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d28ca-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="d28ca-113">Pobieranie samouczek Wprowadzenie, łącznie z tworzeniem magazynu kluczy dla kluczy chronionych modułem HSM, zobacz [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d28ca-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="d28ca-114">Więcej informacji na temat Generowanie i przenoszenie klucza chronionego przez moduł HSM za pośrednictwem Internetu hello:</span><span class="sxs-lookup"><span data-stu-id="d28ca-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="d28ca-115">W trybie offline stację roboczą, co zmniejsza możliwości ataku hello jest generowanie klucza hello.</span><span class="sxs-lookup"><span data-stu-id="d28ca-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="d28ca-116">klucz Hello jest szyfrowany z klucza wymiany klucza (KEK), który pozostaje zaszyfrowany, dopóki nie zostanie przeniesione toohello modułów HSM usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d28ca-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="d28ca-117">Tylko hello zaszyfrowana wersja klucza opuszcza pierwotną stację roboczą hello.</span><span class="sxs-lookup"><span data-stu-id="d28ca-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="d28ca-118">zestaw narzędzi Hello ustawia właściwości klucz dzierżawy, który wiąże się z klucza toohello środowiska zabezpieczeń security world usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d28ca-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="d28ca-119">Dlatego po hello modułów HSM usługi Azure Key Vault odbiorą i odszyfrują klucz, tylko te moduły HSM może być używany.</span><span class="sxs-lookup"><span data-stu-id="d28ca-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="d28ca-120">Nie można wyeksportować klucza.</span><span class="sxs-lookup"><span data-stu-id="d28ca-120">Your key cannot be exported.</span></span> <span data-ttu-id="d28ca-121">To powiązanie jest wymuszone przez hello sprzętowych modułów zabezpieczeń firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="d28ca-122">Witaj klucza wymiany klucza (KEK), który jest używany tooencrypt klucz jest generowany wewnątrz hello modułów HSM usługi Azure Key Vault i nie jest możliwy do eksportu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="d28ca-123">Moduły HSM Hello wymusić nie był dostępny nie ma wersji wyczyść hello KEK poza hello sprzętowych modułów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d28ca-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="d28ca-124">Ponadto hello zestaw narzędzi zawiera zaświadczenie od firmy Thales tego hello KEK nie można wyeksportować i został wygenerowany w oryginalnym module HSM, który wyprodukowanego przez firmę Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="d28ca-125">Witaj zestaw narzędzi zawiera zaświadczenie od firmy Thales tego hello Azure Key Vault środowiska zabezpieczeń security world zostało także wygenerowane w oryginalnym sprzętowym module zabezpieczeń wyprodukowanym przez firmę Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="d28ca-126">To poświadczenie okaże się tooyou, że firma Microsoft korzysta z oryginalnego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="d28ca-127">Firma Microsoft używa oddzielnych kluczy Kek i oddzielne środowiska Security World w każdym regionie geograficznym.</span><span class="sxs-lookup"><span data-stu-id="d28ca-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="d28ca-128">Ta separacja gwarantuje, że klucz może służyć wyłącznie w centrach danych w regionie hello, w którym został zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="d28ca-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="d28ca-129">Na przykład klucz Europejskiego klienta nie można użyć w centrach danych w Ameryce Północnej ani Azji.</span><span class="sxs-lookup"><span data-stu-id="d28ca-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="d28ca-130">Więcej informacji na temat sprzętowych modułów zabezpieczeń firmy Thales i usług firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="d28ca-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="d28ca-131">Firmy Thales e-Security jest wiodącym globalnym dostawcą szyfrowania danych i usług finansowych toohello rozwiązań zabezpieczeń przez, zaawansowanych technologii, produkcyjnym, dla instytucji rządowych i sektorów technologii.</span><span class="sxs-lookup"><span data-stu-id="d28ca-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="d28ca-132">40 lat udokumentowanego doświadczenia ochrony firmy i informacje dla instytucji rządowych rozwiązania firmy Thales są używane przez cztery hello pięć największe energii i aerospace firmy.</span><span class="sxs-lookup"><span data-stu-id="d28ca-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="d28ca-133">Ich rozwiązania są również używane przez 22 kraje NATO, a secure ponad 80 procent transakcji płatniczych na świecie.</span><span class="sxs-lookup"><span data-stu-id="d28ca-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="d28ca-134">Firma Microsoft podjęła współpracę ze stanem hello tooenhance firmy Thales wiedzę w zakresie sprzętowych modułów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d28ca-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="d28ca-135">Te ulepszenia umożliwiają tooget hello typowych zalet usług hostowanych bez potrzeby rezygnacji z kontroli nad kluczami.</span><span class="sxs-lookup"><span data-stu-id="d28ca-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="d28ca-136">W szczególności ulepszenia te umożliwiają firmie Microsoft Zarządzanie hello sprzętowych modułów zabezpieczeń, dzięki czemu nie trzeba.</span><span class="sxs-lookup"><span data-stu-id="d28ca-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="d28ca-137">Jako chmury usługi, usługi Azure Key Vault skaluje w krótkim czasie toomeet wzrósł użytkowania Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="d28ca-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="d28ca-138">At hello sam czasu klucz jest chroniony wewnątrz sprzętowych modułów zabezpieczeń firmy Microsoft: użytkownik zachowuje kontrolę nad hello cyklu życia klucza, ponieważ generowanie klucza hello i przenieść na tooMicrosoft sprzętowych modułów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d28ca-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="d28ca-139">Implementowanie Użyj własnego klucza (BYOK) dla usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d28ca-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="d28ca-140">Użyj hello następujące informacje i procedury, jeśli będzie generowanie własnego klucza chronionego przez moduł HSM, a następnie przenieść je tooAzure Key Vault — Witaj Przełącz scenariusz klucza (BYOK).</span><span class="sxs-lookup"><span data-stu-id="d28ca-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="d28ca-141">Wymagania wstępne dotyczące funkcji BYOK</span><span class="sxs-lookup"><span data-stu-id="d28ca-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="d28ca-142">Zobacz hello w poniższej tabeli, aby uzyskać listę wymagań wstępnych dotyczących Użyj własnego klucza (BYOK) dla usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d28ca-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="d28ca-143">Wymaganie</span><span class="sxs-lookup"><span data-stu-id="d28ca-143">Requirement</span></span> | <span data-ttu-id="d28ca-144">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="d28ca-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="d28ca-145">TooAzure subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d28ca-145">A subscription tooAzure</span></span> |<span data-ttu-id="d28ca-146">toocreate usługi Azure Key Vault, potrzebujesz subskrypcji platformy Azure: [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="d28ca-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="d28ca-147">Witaj kluczy chronionego przez moduł HSM toosupport warstwy usługi Azure klucza magazynu w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="d28ca-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="d28ca-148">Aby uzyskać więcej informacji o hello warstwy usług i możliwości usługi Azure Key Vault, zobacz hello [cennik usługi Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d28ca-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="d28ca-149">Modułu HSM firmy Thales, karty inteligentne i oprogramowanie</span><span class="sxs-lookup"><span data-stu-id="d28ca-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="d28ca-150">Musi mieć dostęp do tooa sprzętowego modułu zabezpieczeń firmy Thales i podstawowe wiedzę na temat działania sprzętowych modułów zabezpieczeń firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="d28ca-151">Zobacz [sprzętowego modułu zabezpieczeń firmy Thales](https://www.thales-esecurity.com/msrms/buy) hello lista zgodnych modeli lub toopurchase modułu HSM, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="d28ca-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="d28ca-152">Witaj następujący sprzęt i oprogramowanie:</span><span class="sxs-lookup"><span data-stu-id="d28ca-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="d28ca-153">W trybie offline x64 stacja robocza z systemem operacyjnym Windows z systemem Windows 7 oraz oprogramowaniem Thales nShield w wersji 11.50.</span><span class="sxs-lookup"><span data-stu-id="d28ca-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="d28ca-154">Jeśli stacja robocza z systemem Windows 7, należy najpierw [instalacja programu Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="d28ca-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="d28ca-155">Stacja robocza toohello połączenia internetowego i ma system operacyjny Windows Windows 7 i [programu Azure PowerShell](/powershell/azure/overview) **minimalna wersja 1.1.0** zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="d28ca-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="d28ca-156">Dysk USB lub inne przenośne urządzenie pamięci masowej z co najmniej 16 MB wolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="d28ca-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="d28ca-157">Ze względów bezpieczeństwa zaleca się pierwsza stacja robocza tego hello nie jest połączony tooa sieci.</span><span class="sxs-lookup"><span data-stu-id="d28ca-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="d28ca-158">Jednak to zalecenie nie jest programowo wymuszana.</span><span class="sxs-lookup"><span data-stu-id="d28ca-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="d28ca-159">Należy pamiętać, że w postępuj zgodnie z instrukcjami hello tej stacji roboczej stacji roboczej hello odłączony tooas określony.</span><span class="sxs-lookup"><span data-stu-id="d28ca-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="d28ca-160">Ponadto jeśli klucz dzierżawy jest przeznaczony dla środowiska produkcyjnego, zaleca się użycie drugiej, oddzielnej stacji roboczej toodownload hello zestaw narzędzi i przekazywanie hello klucz dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="d28ca-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="d28ca-161">Do celów testowych można używać hello stacji roboczej, jako hello pierwsza z nich.</span><span class="sxs-lookup"><span data-stu-id="d28ca-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="d28ca-162">Należy pamiętać, że w postępuj zgodnie z instrukcjami hello druga stacja robocza stacji roboczej określonego tooas hello podłączonej do Internetu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="d28ca-163">Generowanie i przenoszenie z tooAzure klucza HSM magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="d28ca-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="d28ca-164">Będą używać hello następujące pięć toogenerate kroki i transfer Twojego klucza tooan modułu HSM usługi Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="d28ca-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="d28ca-165">Krok 1: Przygotowanie stacji roboczej podłączonej do Internetu</span><span class="sxs-lookup"><span data-stu-id="d28ca-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="d28ca-166">Krok 2: Przygotowanie odłączonej stacji roboczej</span><span class="sxs-lookup"><span data-stu-id="d28ca-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="d28ca-167">Krok 3: Generowanie klucza</span><span class="sxs-lookup"><span data-stu-id="d28ca-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="d28ca-168">Krok 4: Przygotowanie klucza do przeniesienia</span><span class="sxs-lookup"><span data-stu-id="d28ca-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="d28ca-169">Krok 5: Transfer z tooAzure klucza Key Vault</span><span class="sxs-lookup"><span data-stu-id="d28ca-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="d28ca-170">Krok 1: Przygotowanie stacji roboczej podłączonej do Internetu</span><span class="sxs-lookup"><span data-stu-id="d28ca-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="d28ca-171">W tym kroku pierwszego hello procedur przedstawionych na stacji roboczej, który jest połączony toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="d28ca-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="d28ca-172">Krok 1.1: Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d28ca-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="d28ca-173">Stacji roboczej podłączonej do Internetu hello Pobierz i zainstaluj hello modułu Azure PowerShell, która obejmuje hello toomanage poleceń cmdlet usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d28ca-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="d28ca-174">Wymaga minimalnej wersji 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="d28ca-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="d28ca-175">Aby uzyskać instrukcje instalacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d28ca-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="d28ca-176">Krok 1.2: Pobieranie identyfikator subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d28ca-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="d28ca-177">Uruchom sesję programu PowerShell Azure i zaloguj się przy użyciu następującego polecenia hello tooyour konto platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d28ca-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="d28ca-178">W oknie wyskakującym przeglądarki hello wprowadź nazwę użytkownika konta platformy Azure i hasło.</span><span class="sxs-lookup"><span data-stu-id="d28ca-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="d28ca-179">Następnie należy użyć hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) polecenia:</span><span class="sxs-lookup"><span data-stu-id="d28ca-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="d28ca-180">Z danych wyjściowych hello zlokalizuj identyfikator hello hello subskrypcji, które będą używane dla usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d28ca-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="d28ca-181">Ta Subskrypcja będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="d28ca-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="d28ca-182">Nie zamykaj okna programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="d28ca-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="d28ca-183">Krok 1.3: Pobierz hello zestawu narzędzi BYOK dla usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d28ca-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="d28ca-184">Przejdź toohello Microsoft Download Center i [pobrania zestawu narzędzi BYOK magazynu kluczy Azure hello](http://www.microsoft.com/download/details.aspx?id=45345) regionu geograficznego lub wystąpienia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d28ca-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="d28ca-185">Witaj poniższych informacji tooidentify hello pakietu Nazwa toodownload i jego odpowiedniego algorytmu SHA-256 pakietu wyznaczania wartości skrótu:</span><span class="sxs-lookup"><span data-stu-id="d28ca-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="d28ca-186">**Stany Zjednoczone:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-186">**United States:**</span></span>

<span data-ttu-id="d28ca-187">States.zip KeyVault-BYOK-Tools Zjednoczone</span><span class="sxs-lookup"><span data-stu-id="d28ca-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="d28ca-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="d28ca-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="d28ca-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-189">**Europe:**</span></span>

<span data-ttu-id="d28ca-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="d28ca-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="d28ca-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="d28ca-192">**Azja:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-192">**Asia:**</span></span>

<span data-ttu-id="d28ca-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="d28ca-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="d28ca-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="d28ca-195">**Ameryka Łacińska:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-195">**Latin America:**</span></span>

<span data-ttu-id="d28ca-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="d28ca-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="d28ca-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="d28ca-198">**Japonia:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-198">**Japan:**</span></span>

<span data-ttu-id="d28ca-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="d28ca-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="d28ca-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="d28ca-201">**Korea:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-201">**Korea:**</span></span>

<span data-ttu-id="d28ca-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="d28ca-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="d28ca-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="d28ca-204">**Australia:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-204">**Australia:**</span></span>

<span data-ttu-id="d28ca-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="d28ca-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="d28ca-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="d28ca-207">**Azure dla instytucji rządowych:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="d28ca-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="d28ca-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="d28ca-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="d28ca-210">**Dla instytucji rządowych USA DOD:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-210">**US Government DOD:**</span></span>

<span data-ttu-id="d28ca-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="d28ca-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="d28ca-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="d28ca-213">**Kanada:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-213">**Canada:**</span></span>

<span data-ttu-id="d28ca-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="d28ca-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="d28ca-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="d28ca-216">**Niemcy:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-216">**Germany:**</span></span>

<span data-ttu-id="d28ca-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="d28ca-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="d28ca-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="d28ca-219">**Indie:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-219">**India:**</span></span>

<span data-ttu-id="d28ca-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="d28ca-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="d28ca-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="d28ca-222">**Wielka Brytania:**</span><span class="sxs-lookup"><span data-stu-id="d28ca-222">**United Kingdom:**</span></span>

<span data-ttu-id="d28ca-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="d28ca-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="d28ca-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="d28ca-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="d28ca-225">integralność hello toovalidate Twojego pobranego zestawu narzędzi BYOK, w sesji programu Azure PowerShell, użyj hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d28ca-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="d28ca-226">Witaj zestaw narzędzi zawiera następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d28ca-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="d28ca-227">Pakiet klucza wymiany klucza (KEK), którego nazwa zaczyna się od **BYOK-KEK - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="d28ca-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="d28ca-228">Pakiet środowiska zabezpieczeń Security World, którego nazwa zaczyna się od **BYOK-SecurityWorld - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="d28ca-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="d28ca-229">Skrypt w języku python o nazwie **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="d28ca-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="d28ca-230">Plik wykonywalny wiersza polecenia o nazwie **KeyTransferRemote.exe** oraz skojarzone biblioteki dll.</span><span class="sxs-lookup"><span data-stu-id="d28ca-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="d28ca-231">Pakiet redystrybucyjny Visual C++, o nazwie **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="d28ca-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="d28ca-232">Kopiuj hello pakietu tooa USB lub innego przenośnego urządzenia pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="d28ca-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="d28ca-233">Krok 2: Przygotowanie odłączonej stacji roboczej</span><span class="sxs-lookup"><span data-stu-id="d28ca-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="d28ca-234">W tym kroku drugi hello procedur przedstawionych na powitania stacji roboczej, która nie jest siecią połączonych tooa (hello Internetu lub sieci wewnętrznej).</span><span class="sxs-lookup"><span data-stu-id="d28ca-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="d28ca-235">Krok 2.1: Przygotowanie stacji roboczej hello odłączony z modułu HSM firmy Thales</span><span class="sxs-lookup"><span data-stu-id="d28ca-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="d28ca-236">Zainstaluj oprogramowanie wspomagające nCipher (firmy Thales) hello na komputerze z systemem Windows, a następnie dołącz komputer toothat modułu HSM firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="d28ca-237">Upewnij się, że hello narzędzia firmy Thales znajdują się w ścieżce (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="d28ca-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="d28ca-238">Na przykład wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d28ca-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="d28ca-239">Aby uzyskać więcej informacji zobacz Podręcznik użytkownika hello dołączonego hello modułu HSM firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="d28ca-240">Krok 2.2: Zestaw narzędzi BYOK hello instalacji hello odłączony stacji roboczej</span><span class="sxs-lookup"><span data-stu-id="d28ca-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="d28ca-241">Skopiuj pakiet zestawu narzędzi BYOK hello hello dysk USB lub innego przenośnego urządzenia pamięci masowej, a następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d28ca-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="d28ca-242">Wyodrębnij pliki hello z pakietu hello pobrane do dowolnego folderu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="d28ca-243">Uruchom program vcredist_x64.exe z tego folderu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="d28ca-244">Postępuj zgodnie z instrukcjami hello toohello instalują elementy środowiska uruchomieniowego Visual C++ hello for Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d28ca-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="d28ca-245">Krok 3: Generowanie klucza</span><span class="sxs-lookup"><span data-stu-id="d28ca-245">Step 3: Generate your key</span></span>
<span data-ttu-id="d28ca-246">W tym kroku trzeci hello procedur przedstawionych na stacji roboczej hello odłączony.</span><span class="sxs-lookup"><span data-stu-id="d28ca-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="d28ca-247">toocomplete ten krok modułu HSM musi być w trybie inicjowania.</span><span class="sxs-lookup"><span data-stu-id="d28ca-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="d28ca-248">Krok 3.1: Zmień hello HSM tryb too'I "</span><span class="sxs-lookup"><span data-stu-id="d28ca-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="d28ca-249">Jeśli używasz nShield firmy Thales krawędzi, tryb hello toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="d28ca-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="d28ca-250">W trybie hello tryb przycisku toohighlight hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="d28ca-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="d28ca-251">2.</span><span class="sxs-lookup"><span data-stu-id="d28ca-251">2.</span></span> <span data-ttu-id="d28ca-252">W ciągu kilku sekund naciśnij i przytrzymaj ją przycisk Wyczyść hello kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="d28ca-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="d28ca-253">W przypadku zmiany trybu hello, hello LED nowy tryb zatrzymuje miga i pozostaje podświetlone.</span><span class="sxs-lookup"><span data-stu-id="d28ca-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="d28ca-254">Hello LED stanu może flash nieregularnych przez kilka sekund i następnie miga regularnie, gdy urządzenie hello jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="d28ca-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="d28ca-255">W przeciwnym razie hello urządzenie pozostaje w bieżącym trybie hello z hello odpowiedni tryb LED włączone.</span><span class="sxs-lookup"><span data-stu-id="d28ca-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="d28ca-256">Krok 3.2: Utworzenie środowiska zabezpieczeń security world</span><span class="sxs-lookup"><span data-stu-id="d28ca-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="d28ca-257">Uruchom wiersz polecenia i uruchom hello program nowe world firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="d28ca-258">Ten program tworzy **środowiska zabezpieczeń Security World** pliku w lokalizacji % NFAST_KMDATA%\local\world, co odpowiada toohello folderu C:\ProgramData\nCipher\Key Management Data\local.</span><span class="sxs-lookup"><span data-stu-id="d28ca-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="d28ca-259">Można użyć innych wartości dla kworum hello, ale w tym przykładzie użytkownik ma tooenter zostanie wyświetlony monit o trzech pustych kart oraz kodów PIN dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="d28ca-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="d28ca-260">Następnie dowolne dwie spośród kart nadaj środowiska zabezpieczeń security world toohello pełny dostęp.</span><span class="sxs-lookup"><span data-stu-id="d28ca-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="d28ca-261">Te karty stają się hello **zestaw kart administratora** dla hello nowego środowiska zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d28ca-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="d28ca-262">Następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d28ca-262">Then do hello following:</span></span>

* <span data-ttu-id="d28ca-263">Utwórz kopię zapasową hello world pliku.</span><span class="sxs-lookup"><span data-stu-id="d28ca-263">Back up hello world file.</span></span> <span data-ttu-id="d28ca-264">Zabezpieczenia ochrony hello world pliku, hello kart administratora i numerów PIN i upewnij się, że nikt ma toomore dostępu niż jedną kartę.</span><span class="sxs-lookup"><span data-stu-id="d28ca-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="d28ca-265">Krok 3.3: Zmień hello HSM tryb too'O "</span><span class="sxs-lookup"><span data-stu-id="d28ca-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="d28ca-266">Jeśli używasz nShield firmy Thales krawędzi, tryb hello toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="d28ca-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="d28ca-267">W trybie hello tryb przycisku toohighlight hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="d28ca-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="d28ca-268">2.</span><span class="sxs-lookup"><span data-stu-id="d28ca-268">2.</span></span> <span data-ttu-id="d28ca-269">W ciągu kilku sekund naciśnij i przytrzymaj ją przycisk Wyczyść hello kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="d28ca-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="d28ca-270">W przypadku zmiany trybu hello, hello LED nowy tryb zatrzymuje miga i pozostaje podświetlone.</span><span class="sxs-lookup"><span data-stu-id="d28ca-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="d28ca-271">Hello LED stanu może flash nieregularnych przez kilka sekund i następnie miga regularnie, gdy urządzenie hello jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="d28ca-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="d28ca-272">W przeciwnym razie hello urządzenie pozostaje w bieżącym trybie hello z hello odpowiedni tryb LED włączone.</span><span class="sxs-lookup"><span data-stu-id="d28ca-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="d28ca-273">Krok 3.4: Sprawdzanie poprawności pakietu hello pobrane</span><span class="sxs-lookup"><span data-stu-id="d28ca-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="d28ca-274">Ten krok jest opcjonalny, ale zalecany, dzięki czemu można zweryfikować następujących hello:</span><span class="sxs-lookup"><span data-stu-id="d28ca-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="d28ca-275">Hello klucz wymiany klucza jest uwzględniona w hello narzędzi został wygenerowany w oryginalnym module HSM firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="d28ca-276">Skrót Hello hello World zabezpieczeń, uwzględnionej w hello narzędzi został wygenerowany w oryginalnym module HSM firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="d28ca-277">Klucz wymiany klucza Hello jest nie może zostać wyeksportowany.</span><span class="sxs-lookup"><span data-stu-id="d28ca-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="d28ca-278">Witaj toovalidate pobrano pakiet, hello HSM musi być podłączony, włączona i musi mieć zabezpieczeń security world na nim (na przykład hello jedną właśnie utworzone).</span><span class="sxs-lookup"><span data-stu-id="d28ca-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="d28ca-279">Pakiet pobrany hello toovalidate:</span><span class="sxs-lookup"><span data-stu-id="d28ca-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="d28ca-280">Uruchom skrypt verifykeypackage.py hello wpisując jedną z następujących hello, zależnie od regionu geograficznego i wystąpienia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d28ca-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="d28ca-281">Dla Ameryki Północnej:</span><span class="sxs-lookup"><span data-stu-id="d28ca-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="d28ca-282">Dla Europy:</span><span class="sxs-lookup"><span data-stu-id="d28ca-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="d28ca-283">Dla Azji:</span><span class="sxs-lookup"><span data-stu-id="d28ca-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="d28ca-284">Dla Ameryka Łacińska:</span><span class="sxs-lookup"><span data-stu-id="d28ca-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="d28ca-285">W Japonii:</span><span class="sxs-lookup"><span data-stu-id="d28ca-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="d28ca-286">W przypadku Korei:</span><span class="sxs-lookup"><span data-stu-id="d28ca-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="d28ca-287">Dla Australii:</span><span class="sxs-lookup"><span data-stu-id="d28ca-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="d28ca-288">Dla [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych hello USA Azure:</span><span class="sxs-lookup"><span data-stu-id="d28ca-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="d28ca-289">Dla instytucji rządowych USA DOD:</span><span class="sxs-lookup"><span data-stu-id="d28ca-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="d28ca-290">Dla Kanady:</span><span class="sxs-lookup"><span data-stu-id="d28ca-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="d28ca-291">Niemcy:</span><span class="sxs-lookup"><span data-stu-id="d28ca-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="d28ca-292">Dla Indie:</span><span class="sxs-lookup"><span data-stu-id="d28ca-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="d28ca-293">Witaj oprogramowanie firmy Thales obejmuje python w %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="d28ca-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="d28ca-294">Upewnij się, zobacz temat hello następujący komunikat, który wskazuje pomyślnym zweryfikowaniem: **wynik: powodzenie**</span><span class="sxs-lookup"><span data-stu-id="d28ca-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="d28ca-295">Ten skrypt sprawdza łańcuch osoby podpisującej hello się toohello klucza głównego firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="d28ca-296">Hello skrót klucza głównego jest osadzony w skrypcie hello i jego wartość powinna wynosić **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="d28ca-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="d28ca-297">Można również potwierdzić tę wartość osobno, odwiedzając hello [witryny sieci Web firmy Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="d28ca-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="d28ca-298">Możesz teraz gotowy toocreate nowy klucz.</span><span class="sxs-lookup"><span data-stu-id="d28ca-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="d28ca-299">Krok 3.5: Utwórz nowy klucz</span><span class="sxs-lookup"><span data-stu-id="d28ca-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="d28ca-300">Generowanie klucza za pomocą hello firmy Thales **generatekey** programu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="d28ca-301">Uruchom powitania po klucz hello toogenerate polecenia:</span><span class="sxs-lookup"><span data-stu-id="d28ca-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="d28ca-302">Po uruchomieniu tego polecenia, użyj tych instrukcji:</span><span class="sxs-lookup"><span data-stu-id="d28ca-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="d28ca-303">Witaj parametru *chronić* należy ustawić wartość toohello **modułu**, jak pokazano.</span><span class="sxs-lookup"><span data-stu-id="d28ca-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="d28ca-304">Spowoduje to utworzenie klucza chronionego przez moduł.</span><span class="sxs-lookup"><span data-stu-id="d28ca-304">This creates a module-protected key.</span></span> <span data-ttu-id="d28ca-305">Witaj zestawu narzędzi BYOK nie obsługuje klucze chronione przez OCS.</span><span class="sxs-lookup"><span data-stu-id="d28ca-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="d28ca-306">Zastąp wartość hello *contosokey* dla hello **ident** i **plainname** z dowolną wartością ciągu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="d28ca-307">toominimize ogólne koszty administracyjne i zmniejszyć ryzyko hello błędów, zalecane jest użycie hello samą wartość dla obu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="d28ca-308">Witaj **ident** wartość musi zawierać tylko cyfry, łączniki i małych liter.</span><span class="sxs-lookup"><span data-stu-id="d28ca-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="d28ca-309">Parametr Hello pubexp został pozostawiony pusty (wartość domyślna), w tym przykładzie, ale można określić konkretne jego wartości.</span><span class="sxs-lookup"><span data-stu-id="d28ca-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="d28ca-310">Aby uzyskać więcej informacji, zobacz hello dokumentacji firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="d28ca-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="d28ca-311">To polecenie tworzy plik Stokenizowanego klucza w folderze %NFAST_KMDATA%\local o nazwach rozpoczynających z **key_simple_**, a następnie hello **ident** podany w poleceniu hello.</span><span class="sxs-lookup"><span data-stu-id="d28ca-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="d28ca-312">Na przykład: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="d28ca-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="d28ca-313">Ten plik zawiera zaszyfrowany klucz.</span><span class="sxs-lookup"><span data-stu-id="d28ca-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="d28ca-314">Utwórz kopię zapasową tego pliku Stokenizowanego klucza w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="d28ca-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d28ca-315">Po późniejszym przekazaniu Twojej tooAzure klucza Key Vault, Microsoft nie może wyeksportować tego klucza zapasowego tooyou tak ważne bezpiecznie kopii zapasowej z klucza oraz środowiska zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d28ca-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="d28ca-316">Skontaktuj się z firmą Thales wskazówki i najlepsze rozwiązania dotyczące tworzenia kopii zapasowej klucza.</span><span class="sxs-lookup"><span data-stu-id="d28ca-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="d28ca-317">Możesz są teraz gotowe tootransfer Twojego klucza tooAzure magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="d28ca-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="d28ca-318">Krok 4: Przygotowanie klucza do przeniesienia</span><span class="sxs-lookup"><span data-stu-id="d28ca-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="d28ca-319">W tym kroku czwarty hello procedur przedstawionych na stacji roboczej hello odłączony.</span><span class="sxs-lookup"><span data-stu-id="d28ca-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="d28ca-320">Krok 4.1: Utwórz kopię klucza z ograniczonymi uprawnieniami</span><span class="sxs-lookup"><span data-stu-id="d28ca-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="d28ca-321">Otwórz nowy wiersz polecenia i zmień hello bieżącego katalogu toohello lokalizację gdzie można rozpakować pliku zip BYOK hello.</span><span class="sxs-lookup"><span data-stu-id="d28ca-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="d28ca-322">uprawnienia hello tooreduce na klucz, w wierszu polecenia Uruchom jedno z następujących hello, zależnie od regionu geograficznego i wystąpienie usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="d28ca-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="d28ca-323">Dla Ameryki Północnej:</span><span class="sxs-lookup"><span data-stu-id="d28ca-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="d28ca-324">Dla Europy:</span><span class="sxs-lookup"><span data-stu-id="d28ca-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="d28ca-325">Dla Azji:</span><span class="sxs-lookup"><span data-stu-id="d28ca-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="d28ca-326">Dla Ameryka Łacińska:</span><span class="sxs-lookup"><span data-stu-id="d28ca-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="d28ca-327">W Japonii:</span><span class="sxs-lookup"><span data-stu-id="d28ca-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="d28ca-328">W przypadku Korei:</span><span class="sxs-lookup"><span data-stu-id="d28ca-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="d28ca-329">Dla Australii:</span><span class="sxs-lookup"><span data-stu-id="d28ca-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="d28ca-330">Dla [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych hello USA Azure:</span><span class="sxs-lookup"><span data-stu-id="d28ca-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="d28ca-331">Dla instytucji rządowych USA DOD:</span><span class="sxs-lookup"><span data-stu-id="d28ca-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="d28ca-332">Dla Kanady:</span><span class="sxs-lookup"><span data-stu-id="d28ca-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="d28ca-333">Niemcy:</span><span class="sxs-lookup"><span data-stu-id="d28ca-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="d28ca-334">Dla Indie:</span><span class="sxs-lookup"><span data-stu-id="d28ca-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="d28ca-335">Podczas uruchamiania tego polecenia Zastąp *contosokey* z hello samą wartość podana w **3.5 krok: Utwórz nowy klucz** z hello [generowanie klucza](#step-3-generate-your-key) kroku.</span><span class="sxs-lookup"><span data-stu-id="d28ca-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="d28ca-336">Zostanie wyświetlona prośba tooplug w world kart administratora zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d28ca-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="d28ca-337">Gdy hello zakończeniu wykonywania polecenia zostanie wyświetlony **wynik: powodzenie** i hello kopii klucza z ograniczonymi uprawnieniami znajdują się w pliku hello o nazwie key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="d28ca-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="d28ca-338">Może przeprowadzający hello listy ACL za pomocą następujących poleceń przy użyciu hello narzędzia firmy Thales:</span><span class="sxs-lookup"><span data-stu-id="d28ca-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="d28ca-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="d28ca-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="d28ca-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="d28ca-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="d28ca-341">Po uruchomieniu tych poleceń Zastąp contosokey hello samą wartość podana w **3.5 krok: Utwórz nowy klucz** z hello [generowanie klucza](#step-3-generate-your-key) kroku.</span><span class="sxs-lookup"><span data-stu-id="d28ca-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="d28ca-342">Krok 4.2: Zaszyfrowanie klucza przy użyciu klucza wymiany kluczy firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="d28ca-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="d28ca-343">Uruchom jedno z hello następujące polecenia, zależnie od regionu geograficznego i wystąpienie usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="d28ca-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="d28ca-344">Dla Ameryki Północnej:</span><span class="sxs-lookup"><span data-stu-id="d28ca-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-345">Dla Europy:</span><span class="sxs-lookup"><span data-stu-id="d28ca-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-346">Dla Azji:</span><span class="sxs-lookup"><span data-stu-id="d28ca-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-347">Dla Ameryka Łacińska:</span><span class="sxs-lookup"><span data-stu-id="d28ca-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-348">W Japonii:</span><span class="sxs-lookup"><span data-stu-id="d28ca-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-349">W przypadku Korei:</span><span class="sxs-lookup"><span data-stu-id="d28ca-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-350">Dla Australii:</span><span class="sxs-lookup"><span data-stu-id="d28ca-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-351">Dla [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych hello USA Azure:</span><span class="sxs-lookup"><span data-stu-id="d28ca-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-352">Dla instytucji rządowych USA DOD:</span><span class="sxs-lookup"><span data-stu-id="d28ca-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-353">Dla Kanady:</span><span class="sxs-lookup"><span data-stu-id="d28ca-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-354">Niemcy:</span><span class="sxs-lookup"><span data-stu-id="d28ca-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d28ca-355">Dla Indie:</span><span class="sxs-lookup"><span data-stu-id="d28ca-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="d28ca-356">Po uruchomieniu tego polecenia, użyj tych instrukcji:</span><span class="sxs-lookup"><span data-stu-id="d28ca-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="d28ca-357">Zastąp *contosokey* używany klucz hello toogenerate w identyfikatorze hello **3.5 krok: Utwórz nowy klucz** z hello [generowanie klucza](#step-3-generate-your-key) kroku.</span><span class="sxs-lookup"><span data-stu-id="d28ca-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="d28ca-358">Zastąp *SubscriptionID* o identyfikatorze hello hello subskrypcji Azure, która zawiera magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="d28ca-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="d28ca-359">Tę wartość można pobrać wcześniej w **kroku 1.2: Uzyskaj identyfikator subskrypcji platformy Azure** z hello [Przygotowanie stacji roboczej podłączonej do Internetu](#step-1-prepare-your-internet-connected-workstation) krok.</span><span class="sxs-lookup"><span data-stu-id="d28ca-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="d28ca-360">Zastąp *ContosoFirstHSMKey* etykietą, która jest używana do nazwy pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="d28ca-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="d28ca-361">Po pomyślnym zakończeniu, wyświetla **wynik: powodzenie** i ma nowy plik w folderze bieżącego hello, który ma hello następującej nazwie: KeyTransferPackage -*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="d28ca-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="d28ca-362">Krok 4.3: Przekazanie klucza pakietu toohello połączony z Internetem stacji roboczej do kopiowania</span><span class="sxs-lookup"><span data-stu-id="d28ca-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="d28ca-363">Użyj dysku USB lub innego przenośnego urządzenia pamięci masowej toocopy hello wyjściowego pliku hello poprzedniego kroku (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour połączony z Internetem stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="d28ca-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="d28ca-364">Krok 5: Transfer z tooAzure klucza Key Vault</span><span class="sxs-lookup"><span data-stu-id="d28ca-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="d28ca-365">Ten ostatni krok na stacji roboczej podłączonej do Internetu hello, użyć hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) pakietu przekazywania klucza hello tooupload polecenia cmdlet, skopiowany z hello odłączony toohello stacji roboczej modułu HSM usługi Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="d28ca-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="d28ca-366">Jeśli przekazywanie hello zakończy się pomyślnie, zobaczysz właściwości wyświetlane hello hello klucza, który właśnie został dodany.</span><span class="sxs-lookup"><span data-stu-id="d28ca-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d28ca-367">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d28ca-367">Next steps</span></span>
<span data-ttu-id="d28ca-368">Można teraz używać tego klucza chronionego przez moduł HSM w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="d28ca-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="d28ca-369">Aby uzyskać więcej informacji, zobacz hello **Jeśli chcesz toouse sprzętowego modułu zabezpieczeń (HSM)** części hello [wprowadzenie do korzystania z usługi Azure Key Vault](key-vault-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="d28ca-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
