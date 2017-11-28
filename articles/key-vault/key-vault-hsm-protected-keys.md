---
title: "Jak Generowanie i przenoszenie kluczy chronionych modułem HSM dla usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Użyj w tym artykule, aby ułatwić planowanie, generowanie, a następnie przenieść własne klucze chronione przez moduł HSM do użycia z usługą Azure Key Vault. Znany również jako BYOK lub własnego klucza."
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
ms.openlocfilehash: 5dbee1221f64045c64fecb344de1e03b2183dfb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-generate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="abdb2-104">Jak Generowanie i przenoszenie chronionego przez moduł HSM kluczy dla usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="abdb2-104">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="abdb2-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="abdb2-105">Introduction</span></span>
<span data-ttu-id="abdb2-106">Dla dodatkowego bezpieczeństwa korzystając z usługi Azure Key Vault, można zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM.</span><span class="sxs-lookup"><span data-stu-id="abdb2-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="abdb2-107">Ten scenariusz jest często określany jako *własnego klucza*, byok.</span><span class="sxs-lookup"><span data-stu-id="abdb2-107">This scenario is often referred to as *bring your own key*, or BYOK.</span></span> <span data-ttu-id="abdb2-108">Moduły HSM są zweryfikowane w trybie FIPS 140-2 poziom 2.</span><span class="sxs-lookup"><span data-stu-id="abdb2-108">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="abdb2-109">Usługa Azure Key Vault używa rodziny nShield firmy Thales sprzętowych modułów zabezpieczeń do ochrony kluczy.</span><span class="sxs-lookup"><span data-stu-id="abdb2-109">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span></span>

<span data-ttu-id="abdb2-110">Skorzystaj z informacji w tym temacie, aby ułatwić planowanie, generowanie, a następnie przenieść własne klucze chronione przez moduł HSM do użycia z usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="abdb2-110">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>

<span data-ttu-id="abdb2-111">Ta funkcja nie jest dostępna dla Chińskiej wersji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="abdb2-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="abdb2-112">Aby uzyskać więcej informacji na temat usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="abdb2-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="abdb2-113">Pobieranie samouczek Wprowadzenie, łącznie z tworzeniem magazynu kluczy dla kluczy chronionych modułem HSM, zobacz [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="abdb2-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="abdb2-114">Więcej informacji na temat Generowanie i przenoszenie klucza chronionego przez moduł HSM za pośrednictwem Internetu:</span><span class="sxs-lookup"><span data-stu-id="abdb2-114">More information about generating and transferring an HSM-protected key over the Internet:</span></span>

* <span data-ttu-id="abdb2-115">Generowania klucza w trybie offline stację roboczą, co zmniejsza możliwości ataku.</span><span class="sxs-lookup"><span data-stu-id="abdb2-115">You generate the key from an offline workstation, which reduces the attack surface.</span></span>
* <span data-ttu-id="abdb2-116">Klucz jest zaszyfrowany z klucza wymiany klucza (KEK), który pozostaje zaszyfrowany, dopóki nie zostanie przesłany do modułów HSM usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="abdb2-116">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span></span> <span data-ttu-id="abdb2-117">Wyłącznie zaszyfrowana wersja klucza opuszcza pierwotną stację roboczą.</span><span class="sxs-lookup"><span data-stu-id="abdb2-117">Only the encrypted version of your key leaves the original workstation.</span></span>
* <span data-ttu-id="abdb2-118">Zestaw narzędzi ustawia właściwości klucz dzierżawy, który wiąże klucz do środowiska zabezpieczeń security world usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="abdb2-118">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span></span> <span data-ttu-id="abdb2-119">Dlatego po modułów HSM usługi Azure Key Vault odbiorą i odszyfrują klucz, tylko te moduły HSM może być używany.</span><span class="sxs-lookup"><span data-stu-id="abdb2-119">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="abdb2-120">Nie można wyeksportować klucza.</span><span class="sxs-lookup"><span data-stu-id="abdb2-120">Your key cannot be exported.</span></span> <span data-ttu-id="abdb2-121">To powiązanie jest wymuszone przez moduły HSM firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-121">This binding is enforced by the Thales HSMs.</span></span>
* <span data-ttu-id="abdb2-122">Klucz wymiany klucza (KEK), który jest używany do szyfrowania klucza jest generowany wewnątrz modułów HSM usługi Azure Key Vault i nie jest możliwy do eksportu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-122">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="abdb2-123">Sprzętowe moduły zabezpieczeń wymusić nie był dostępny nie ma wersji wyczyść KEK poza ich obrębem.</span><span class="sxs-lookup"><span data-stu-id="abdb2-123">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span></span> <span data-ttu-id="abdb2-124">Ponadto zestaw narzędzi zawiera zaświadczenie od firmy Thales, że klucza KEK nie można wyeksportować i został wygenerowany w oryginalnym module HSM, który wyprodukowanego przez firmę Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-124">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="abdb2-125">Zestaw narzędzi zawiera zaświadczenie od firmy Thales, że środowiska zabezpieczeń security world usługi Azure Key Vault zostało także wygenerowane w oryginalnym sprzętowym module zabezpieczeń wyprodukowanym przez firmę Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-125">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="abdb2-126">To poświadczenie gwarantuje, że firma Microsoft korzysta z oryginalnego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-126">This attestation proves to you that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="abdb2-127">Firma Microsoft używa oddzielnych kluczy Kek i oddzielne środowiska Security World w każdym regionie geograficznym.</span><span class="sxs-lookup"><span data-stu-id="abdb2-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="abdb2-128">Ta separacja gwarantuje, że klucz może służyć wyłącznie w centrach danych w regionie, w którym został zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="abdb2-128">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span></span> <span data-ttu-id="abdb2-129">Na przykład klucz Europejskiego klienta nie można użyć w centrach danych w Ameryce Północnej ani Azji.</span><span class="sxs-lookup"><span data-stu-id="abdb2-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="abdb2-130">Więcej informacji na temat sprzętowych modułów zabezpieczeń firmy Thales i usług firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="abdb2-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="abdb2-131">Firmy Thales e-Security jest wiodącym globalnym dostawcą szyfrowania danych i rozwiązań zabezpieczeń przez branży usług finansowych, zaawansowanych technologii, produkcyjnym, dla instytucji rządowych i sektorów technologii.</span><span class="sxs-lookup"><span data-stu-id="abdb2-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="abdb2-132">40 lat udokumentowanego doświadczenia ochrony firmy i informacje dla instytucji rządowych że rozwiązania firmy Thales są używane przez cztery pięć największych firm z sektora energetycznego i aerospace.</span><span class="sxs-lookup"><span data-stu-id="abdb2-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span></span> <span data-ttu-id="abdb2-133">Ich rozwiązania są również używane przez 22 kraje NATO, a secure ponad 80 procent transakcji płatniczych na świecie.</span><span class="sxs-lookup"><span data-stu-id="abdb2-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="abdb2-134">Firma Microsoft podjęła współpracę z firmą Thales, aby pogłębić wiedzę do sprzętowych modułów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="abdb2-134">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span></span> <span data-ttu-id="abdb2-135">Te ulepszenia umożliwiają uzyskanie z typowych zalet usług hostowanych bez potrzeby rezygnacji z kontroli nad kluczami.</span><span class="sxs-lookup"><span data-stu-id="abdb2-135">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="abdb2-136">W szczególności ulepszenia te umożliwiają firmie Microsoft Zarządzanie modułów HSM, dzięki czemu nie trzeba.</span><span class="sxs-lookup"><span data-stu-id="abdb2-136">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span></span> <span data-ttu-id="abdb2-137">Usługa w chmurze usługi Azure Key Vault skaluje w krótkim czasie w celu zaspokojenia nagłego Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="abdb2-137">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span></span> <span data-ttu-id="abdb2-138">W tym samym czasie, klucz jest chroniony wewnątrz sprzętowych modułów zabezpieczeń firmy Microsoft: użytkownik zachowuje kontrolę nad cyklu życia klucza, ponieważ klucz wygenerowany i przenieść ją do sprzętowych modułów zabezpieczeń firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="abdb2-138">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="abdb2-139">Implementowanie Użyj własnego klucza (BYOK) dla usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="abdb2-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="abdb2-140">Użyj następujące informacje i procedury, jeśli będzie generowanie własnego klucza chronionego przez moduł HSM, a następnie przenieś ją do usługi Azure Key Vault — bring scenariusz klucza (BYOK).</span><span class="sxs-lookup"><span data-stu-id="abdb2-140">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="abdb2-141">Wymagania wstępne dotyczące funkcji BYOK</span><span class="sxs-lookup"><span data-stu-id="abdb2-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="abdb2-142">Zobacz poniższą tabelę na listę warunków wstępnych, Użyj własnego klucza (BYOK) dla usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="abdb2-142">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="abdb2-143">Wymaganie</span><span class="sxs-lookup"><span data-stu-id="abdb2-143">Requirement</span></span> | <span data-ttu-id="abdb2-144">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="abdb2-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="abdb2-145">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="abdb2-145">A subscription to Azure</span></span> |<span data-ttu-id="abdb2-146">Do utworzenia magazynu kluczy Azure, potrzebujesz subskrypcji platformy Azure: [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="abdb2-146">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="abdb2-147">Warstwy usług Premium magazynu kluczy Azure do obsługi klucze chronione przez moduł HSM</span><span class="sxs-lookup"><span data-stu-id="abdb2-147">The Azure Key Vault Premium service tier to support HSM-protected keys</span></span> |<span data-ttu-id="abdb2-148">Aby uzyskać więcej informacji o warstwy usług i możliwości usługi Azure Key Vault, zobacz [cennik usługi Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="abdb2-148">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="abdb2-149">Modułu HSM firmy Thales, karty inteligentne i oprogramowanie</span><span class="sxs-lookup"><span data-stu-id="abdb2-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="abdb2-150">Musi mieć dostęp do sprzętowego modułu zabezpieczeń firmy Thales i podstawowe wiedzę na temat działania sprzętowych modułów zabezpieczeń firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-150">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="abdb2-151">Zobacz [sprzętowego modułu zabezpieczeń firmy Thales](https://www.thales-esecurity.com/msrms/buy) listę zgodnych modeli lub w celu zakupu sprzętowego, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="abdb2-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="abdb2-152">Następujący sprzęt i oprogramowanie:</span><span class="sxs-lookup"><span data-stu-id="abdb2-152">The following hardware and software:</span></span><ol><li><span data-ttu-id="abdb2-153">W trybie offline x64 stacja robocza z systemem operacyjnym Windows z systemem Windows 7 oraz oprogramowaniem Thales nShield w wersji 11.50.</span><span class="sxs-lookup"><span data-stu-id="abdb2-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="abdb2-154">Jeśli stacja robocza z systemem Windows 7, należy najpierw [instalacja programu Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="abdb2-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="abdb2-155">Stacji roboczej, który jest połączony z Internetem i ma minimalny system operacyjny Windows, Windows 7 i [programu Azure PowerShell](/powershell/azure/overview) **minimalna wersja 1.1.0** zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="abdb2-155">A workstation that is connected to the Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="abdb2-156">Dysk USB lub inne przenośne urządzenie pamięci masowej z co najmniej 16 MB wolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="abdb2-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="abdb2-157">Ze względów bezpieczeństwa zaleca się, że pierwszej stacji roboczej nie jest podłączony do sieci.</span><span class="sxs-lookup"><span data-stu-id="abdb2-157">For security reasons, we recommend that the first workstation is not connected to a network.</span></span> <span data-ttu-id="abdb2-158">Jednak to zalecenie nie jest programowo wymuszana.</span><span class="sxs-lookup"><span data-stu-id="abdb2-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="abdb2-159">Należy pamiętać, że w postępuj zgodnie z instrukcjami stacja robocza jest określana jako odłączonej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="abdb2-159">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="abdb2-160">Ponadto jeśli klucz dzierżawy jest przeznaczony dla środowiska produkcyjnego, zaleca się użyć drugiej, oddzielnej stacji roboczej do pobrania zestawu narzędzi i przesłania klucza dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="abdb2-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span></span> <span data-ttu-id="abdb2-161">Jednak do celów testowych, można użyć tej samej stacji roboczej, jako pierwsza z nich.</span><span class="sxs-lookup"><span data-stu-id="abdb2-161">But for testing purposes, you can use the same workstation as the first one.</span></span><br/><br/><span data-ttu-id="abdb2-162">Należy pamiętać, że w postępuj zgodnie z instrukcjami druga stacja robocza jest określana jako stacji roboczej podłączonej do Internetu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-162">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-to-azure-key-vault-hsm"></a><span data-ttu-id="abdb2-163">Generowanie i przenoszenie klucza do modułu HSM usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="abdb2-163">Generate and transfer your key to Azure Key Vault HSM</span></span>
<span data-ttu-id="abdb2-164">Poniższe kroki pięć umożliwia generowanie i przenoszenie klucza do modułu HSM usługi Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="abdb2-164">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="abdb2-165">Krok 1: Przygotowanie stacji roboczej podłączonej do Internetu</span><span class="sxs-lookup"><span data-stu-id="abdb2-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="abdb2-166">Krok 2: Przygotowanie odłączonej stacji roboczej</span><span class="sxs-lookup"><span data-stu-id="abdb2-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="abdb2-167">Krok 3: Generowanie klucza</span><span class="sxs-lookup"><span data-stu-id="abdb2-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="abdb2-168">Krok 4: Przygotowanie klucza do przeniesienia</span><span class="sxs-lookup"><span data-stu-id="abdb2-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="abdb2-169">Krok 5: Przesłanie klucza do usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="abdb2-169">Step 5: Transfer your key to Azure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="abdb2-170">Krok 1: Przygotowanie stacji roboczej podłączonej do Internetu</span><span class="sxs-lookup"><span data-stu-id="abdb2-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="abdb2-171">Pierwszym kroku wykonaj następujące procedury na stacji roboczej, który jest połączony z Internetem.</span><span class="sxs-lookup"><span data-stu-id="abdb2-171">For this first step, do the following procedures on your workstation that is connected to the Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="abdb2-172">Krok 1.1: Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="abdb2-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="abdb2-173">Od stacji roboczej podłączonej do Internetu Pobierz i zainstaluj moduł Azure PowerShell, który zawiera polecenia cmdlet do zarządzania usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="abdb2-173">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span></span> <span data-ttu-id="abdb2-174">Wymaga minimalnej wersji 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="abdb2-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="abdb2-175">Aby uzyskać instrukcje instalacji, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="abdb2-175">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="abdb2-176">Krok 1.2: Pobieranie identyfikator subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="abdb2-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="abdb2-177">Uruchom sesję programu PowerShell Azure i zaloguj się do konta platformy Azure przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="abdb2-177">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="abdb2-178">W podręcznym oknie przeglądarki wprowadź nazwę użytkownika i hasło dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="abdb2-178">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="abdb2-179">Następnie należy użyć [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) polecenia:</span><span class="sxs-lookup"><span data-stu-id="abdb2-179">Then, use the [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="abdb2-180">Z danych wyjściowych zlokalizuj identyfikator subskrypcji, które będą używane dla usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="abdb2-180">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="abdb2-181">Ta Subskrypcja będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="abdb2-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="abdb2-182">Nie zamykaj okna programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abdb2-182">Do not close the Azure PowerShell window.</span></span>

### <a name="step-13-download-the-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="abdb2-183">Krok 1.3: Pobranie zestawu narzędzi BYOK dla usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="abdb2-183">Step 1.3: Download the BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="abdb2-184">Przejdź do witryny Microsoft Download Center i [pobrania zestawu narzędzi BYOK magazynu kluczy Azure](http://www.microsoft.com/download/details.aspx?id=45345) regionu geograficznego lub wystąpienia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="abdb2-184">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="abdb2-185">Aby zidentyfikować nazwę pakietu do pobrania i jego odpowiedniego skrótu pakietu algorytmu SHA-256, należy użyć następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="abdb2-185">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="abdb2-186">**Stany Zjednoczone:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-186">**United States:**</span></span>

<span data-ttu-id="abdb2-187">States.zip KeyVault-BYOK-Tools Zjednoczone</span><span class="sxs-lookup"><span data-stu-id="abdb2-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="abdb2-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="abdb2-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="abdb2-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-189">**Europe:**</span></span>

<span data-ttu-id="abdb2-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="abdb2-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="abdb2-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="abdb2-192">**Azja:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-192">**Asia:**</span></span>

<span data-ttu-id="abdb2-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="abdb2-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="abdb2-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="abdb2-195">**Ameryka Łacińska:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-195">**Latin America:**</span></span>

<span data-ttu-id="abdb2-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="abdb2-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="abdb2-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="abdb2-198">**Japonia:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-198">**Japan:**</span></span>

<span data-ttu-id="abdb2-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="abdb2-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="abdb2-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="abdb2-201">**Korea:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-201">**Korea:**</span></span>

<span data-ttu-id="abdb2-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="abdb2-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="abdb2-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="abdb2-204">**Australia:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-204">**Australia:**</span></span>

<span data-ttu-id="abdb2-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="abdb2-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="abdb2-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="abdb2-207">**Azure dla instytucji rządowych:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="abdb2-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="abdb2-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="abdb2-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="abdb2-210">**Dla instytucji rządowych USA DOD:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-210">**US Government DOD:**</span></span>

<span data-ttu-id="abdb2-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="abdb2-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="abdb2-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="abdb2-213">**Kanada:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-213">**Canada:**</span></span>

<span data-ttu-id="abdb2-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="abdb2-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="abdb2-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="abdb2-216">**Niemcy:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-216">**Germany:**</span></span>

<span data-ttu-id="abdb2-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="abdb2-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="abdb2-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="abdb2-219">**Indie:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-219">**India:**</span></span>

<span data-ttu-id="abdb2-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="abdb2-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="abdb2-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="abdb2-222">**Wielka Brytania:**</span><span class="sxs-lookup"><span data-stu-id="abdb2-222">**United Kingdom:**</span></span>

<span data-ttu-id="abdb2-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="abdb2-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="abdb2-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="abdb2-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="abdb2-225">Aby zweryfikować integralność z pobranego zestawu narzędzi BYOK, w sesji programu Azure PowerShell, użyj [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="abdb2-225">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="abdb2-226">Zestaw narzędzi zawiera następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="abdb2-226">The toolset includes the following:</span></span>

* <span data-ttu-id="abdb2-227">Pakiet klucza wymiany klucza (KEK), którego nazwa zaczyna się od **BYOK-KEK - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="abdb2-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="abdb2-228">Pakiet środowiska zabezpieczeń Security World, którego nazwa zaczyna się od **BYOK-SecurityWorld - pkg-.**</span><span class="sxs-lookup"><span data-stu-id="abdb2-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="abdb2-229">Skrypt w języku python o nazwie **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="abdb2-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="abdb2-230">Plik wykonywalny wiersza polecenia o nazwie **KeyTransferRemote.exe** oraz skojarzone biblioteki dll.</span><span class="sxs-lookup"><span data-stu-id="abdb2-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="abdb2-231">Pakiet redystrybucyjny Visual C++, o nazwie **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="abdb2-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="abdb2-232">Skopiuj pakiet na dysk USB lub innego przenośnego urządzenia pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="abdb2-232">Copy the package to a USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="abdb2-233">Krok 2: Przygotowanie odłączonej stacji roboczej</span><span class="sxs-lookup"><span data-stu-id="abdb2-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="abdb2-234">Ten krok drugi wykonaj następujące procedury na stacji roboczej, która nie jest podłączony do sieci (Internetu lub sieci wewnętrznej).</span><span class="sxs-lookup"><span data-stu-id="abdb2-234">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span></span>

### <a name="step-21-prepare-the-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="abdb2-235">Krok 2.1: Przygotowanie odłączonej stacji roboczej z modułu HSM firmy Thales</span><span class="sxs-lookup"><span data-stu-id="abdb2-235">Step 2.1: Prepare the disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="abdb2-236">Zainstaluj oprogramowanie wspomagające nCipher (firmy Thales) na komputerze z systemem Windows, a następnie dołącz HSM firmy Thales do komputera.</span><span class="sxs-lookup"><span data-stu-id="abdb2-236">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span></span>

<span data-ttu-id="abdb2-237">Upewnij się, że narzędzia firmy Thales znajdują się w ścieżce (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="abdb2-237">Ensure that the Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="abdb2-238">Na przykład wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="abdb2-238">For example, type the following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="abdb2-239">Aby uzyskać więcej informacji zobacz Podręcznik użytkownika dołączone do modułu HSM firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-239">For more information, see the user guide included with the Thales HSM.</span></span>

### <a name="step-22-install-the-byok-toolset-on-the-disconnected-workstation"></a><span data-ttu-id="abdb2-240">Krok 2.2: Instalacja zestawu narzędzi BYOK na odłączonej stacji roboczej</span><span class="sxs-lookup"><span data-stu-id="abdb2-240">Step 2.2: Install the BYOK toolset on the disconnected workstation</span></span>
<span data-ttu-id="abdb2-241">Skopiuj pakiet zestawu narzędzi BYOK z dysku USB lub innego przenośnego urządzenia pamięci masowej, a następnie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="abdb2-241">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span></span>

1. <span data-ttu-id="abdb2-242">Wyodrębnij pliki z pobranego pakietu do dowolnego folderu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-242">Extract the files from the downloaded package into any folder.</span></span>
2. <span data-ttu-id="abdb2-243">Uruchom program vcredist_x64.exe z tego folderu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="abdb2-244">Postępuj zgodnie z instrukcjami instalacji składników środowiska uruchomieniowego Visual C++ dla programu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="abdb2-244">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="abdb2-245">Krok 3: Generowanie klucza</span><span class="sxs-lookup"><span data-stu-id="abdb2-245">Step 3: Generate your key</span></span>
<span data-ttu-id="abdb2-246">Ten krok trzeci wykonaj następujące procedury na odłączonej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="abdb2-246">For this third step, do the following procedures on the disconnected workstation.</span></span> <span data-ttu-id="abdb2-247">Aby ukończyć ten krok modułu HSM, musi być w trybie inicjowania.</span><span class="sxs-lookup"><span data-stu-id="abdb2-247">To complete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-the-hsm-mode-to-i"></a><span data-ttu-id="abdb2-248">Krok 3.1: Zmień tryb HSM "I"</span><span class="sxs-lookup"><span data-stu-id="abdb2-248">Step 3.1: Change the HSM mode to 'I'</span></span>
<span data-ttu-id="abdb2-249">Jeśli używasz nShield firmy Thales krawędzi, aby zmienić tryb: 1.</span><span class="sxs-lookup"><span data-stu-id="abdb2-249">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="abdb2-250">Przycisk trybu zaznacz opcję Tryb wymagane.</span><span class="sxs-lookup"><span data-stu-id="abdb2-250">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="abdb2-251">2.</span><span class="sxs-lookup"><span data-stu-id="abdb2-251">2.</span></span> <span data-ttu-id="abdb2-252">W ciągu kilku sekund naciśnij i przytrzymaj ją przycisk Wyczyść kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="abdb2-252">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="abdb2-253">W przypadku zmiany trybu, LED nowy tryb zatrzymuje miga i pozostaje podświetlone.</span><span class="sxs-lookup"><span data-stu-id="abdb2-253">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="abdb2-254">LED stanu może flash nieregularnych przez kilka sekund i następnie miga regularnie, gdy urządzenie jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="abdb2-254">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="abdb2-255">W przeciwnym razie urządzenia pozostaje w bieżącym trybie odpowiedni tryb LED włączone.</span><span class="sxs-lookup"><span data-stu-id="abdb2-255">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="abdb2-256">Krok 3.2: Utworzenie środowiska zabezpieczeń security world</span><span class="sxs-lookup"><span data-stu-id="abdb2-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="abdb2-257">Uruchom wiersz polecenia, a następnie uruchom program nowe world firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-257">Start a command prompt and run the Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="abdb2-258">Ten program tworzy **środowiska zabezpieczeń Security World** pliku w lokalizacji % NFAST_KMDATA%\local\world, co odpowiada folderu C:\ProgramData\nCipher\Key Management Data\local.</span><span class="sxs-lookup"><span data-stu-id="abdb2-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="abdb2-259">Można użyć innych wartości dla kworum, ale w tym przykładzie zostanie wyświetlony monit o wprowadzenie trzech pustych kart oraz kodów PIN dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="abdb2-259">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span></span> <span data-ttu-id="abdb2-260">Następnie dowolne dwie spośród kart zapewnić pełny dostęp do środowiska zabezpieczeń security world.</span><span class="sxs-lookup"><span data-stu-id="abdb2-260">Then, any two cards give full access to the security world.</span></span> <span data-ttu-id="abdb2-261">Te karty stają się **zestaw kart administratora** dla nowego środowiska zabezpieczeń security world.</span><span class="sxs-lookup"><span data-stu-id="abdb2-261">These cards become the **Administrator Card Set** for the new security world.</span></span>

<span data-ttu-id="abdb2-262">Następnie wykonaj poniższe czynności:</span><span class="sxs-lookup"><span data-stu-id="abdb2-262">Then do the following:</span></span>

* <span data-ttu-id="abdb2-263">Utwórz kopię zapasową pliku środowiska zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="abdb2-263">Back up the world file.</span></span> <span data-ttu-id="abdb2-264">Zabezpieczenie i ochronę pliku środowiska zabezpieczeń, karty administratora i numerów PIN i upewnij się, że nie jedna osoba ma dostęp do więcej niż jedną kartę.</span><span class="sxs-lookup"><span data-stu-id="abdb2-264">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span></span>

### <a name="step-33-change-the-hsm-mode-to-o"></a><span data-ttu-id="abdb2-265">Krok 3.3: Zmień tryb HSM, aby ' O'</span><span class="sxs-lookup"><span data-stu-id="abdb2-265">Step 3.3: Change the HSM mode to 'O'</span></span>
<span data-ttu-id="abdb2-266">Jeśli używasz nShield firmy Thales krawędzi, aby zmienić tryb: 1.</span><span class="sxs-lookup"><span data-stu-id="abdb2-266">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="abdb2-267">Przycisk trybu zaznacz opcję Tryb wymagane.</span><span class="sxs-lookup"><span data-stu-id="abdb2-267">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="abdb2-268">2.</span><span class="sxs-lookup"><span data-stu-id="abdb2-268">2.</span></span> <span data-ttu-id="abdb2-269">W ciągu kilku sekund naciśnij i przytrzymaj ją przycisk Wyczyść kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="abdb2-269">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="abdb2-270">W przypadku zmiany trybu, LED nowy tryb zatrzymuje miga i pozostaje podświetlone.</span><span class="sxs-lookup"><span data-stu-id="abdb2-270">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="abdb2-271">LED stanu może flash nieregularnych przez kilka sekund i następnie miga regularnie, gdy urządzenie jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="abdb2-271">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="abdb2-272">W przeciwnym razie urządzenia pozostaje w bieżącym trybie odpowiedni tryb LED włączone.</span><span class="sxs-lookup"><span data-stu-id="abdb2-272">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>


### <a name="step-34-validate-the-downloaded-package"></a><span data-ttu-id="abdb2-273">Krok 3.4: Weryfikacja pobranego pakietu</span><span class="sxs-lookup"><span data-stu-id="abdb2-273">Step 3.4: Validate the downloaded package</span></span>
<span data-ttu-id="abdb2-274">Ten krok jest opcjonalny, ale zalecany, aby sprawdzić następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="abdb2-274">This step is optional but recommended so that you can validate the following:</span></span>

* <span data-ttu-id="abdb2-275">Klucz wymiany klucza, który znajduje się w zestawie narzędzi został wygenerowany w oryginalnym module HSM firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-275">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="abdb2-276">Skrót środowiska zabezpieczeń Security World, który znajduje się w zestawie narzędzi został wygenerowany w oryginalnym module HSM firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-276">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="abdb2-277">Klucz wymiany klucza jest nie może zostać wyeksportowany.</span><span class="sxs-lookup"><span data-stu-id="abdb2-277">The Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="abdb2-278">Aby zweryfikować pobrany pakiet, moduł HSM musi być podłączony i włączony i mieć zabezpieczeń security world na nim (na przykład tego, który właśnie został utworzony).</span><span class="sxs-lookup"><span data-stu-id="abdb2-278">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span></span>
>
>

<span data-ttu-id="abdb2-279">Aby zweryfikować pobrany pakiet:</span><span class="sxs-lookup"><span data-stu-id="abdb2-279">To validate the downloaded package:</span></span>

1. <span data-ttu-id="abdb2-280">Uruchom skrypt verifykeypackage.py, wpisując jedną z nich, zależnie od regionu geograficznego i wystąpienia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="abdb2-280">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="abdb2-281">Dla Ameryki Północnej:</span><span class="sxs-lookup"><span data-stu-id="abdb2-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="abdb2-282">Dla Europy:</span><span class="sxs-lookup"><span data-stu-id="abdb2-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="abdb2-283">Dla Azji:</span><span class="sxs-lookup"><span data-stu-id="abdb2-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="abdb2-284">Dla Ameryka Łacińska:</span><span class="sxs-lookup"><span data-stu-id="abdb2-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="abdb2-285">W Japonii:</span><span class="sxs-lookup"><span data-stu-id="abdb2-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="abdb2-286">W przypadku Korei:</span><span class="sxs-lookup"><span data-stu-id="abdb2-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="abdb2-287">Dla Australii:</span><span class="sxs-lookup"><span data-stu-id="abdb2-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="abdb2-288">Aby uzyskać [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych USA Azure:</span><span class="sxs-lookup"><span data-stu-id="abdb2-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="abdb2-289">Dla instytucji rządowych USA DOD:</span><span class="sxs-lookup"><span data-stu-id="abdb2-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="abdb2-290">Dla Kanady:</span><span class="sxs-lookup"><span data-stu-id="abdb2-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="abdb2-291">Niemcy:</span><span class="sxs-lookup"><span data-stu-id="abdb2-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="abdb2-292">Dla Indie:</span><span class="sxs-lookup"><span data-stu-id="abdb2-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="abdb2-293">Oprogramowanie firmy Thales obejmuje python w %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="abdb2-293">The Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="abdb2-294">Upewnij się, że zostanie wyświetlony następujący komunikat, który wskazuje pomyślnym zweryfikowaniem: **wynik: powodzenie**</span><span class="sxs-lookup"><span data-stu-id="abdb2-294">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="abdb2-295">Ten skrypt sprawdza łańcuch osoby podpisującej aż klucza głównego firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-295">This script validates the signer chain up to the Thales root key.</span></span> <span data-ttu-id="abdb2-296">Skrót klucza głównego jest osadzony w skrypcie i jego wartość powinna wynosić **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="abdb2-296">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="abdb2-297">Można również potwierdzić tę wartość osobno, odwiedzając [witryny sieci Web firmy Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="abdb2-297">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="abdb2-298">Teraz możesz utworzyć nowy klucz.</span><span class="sxs-lookup"><span data-stu-id="abdb2-298">You’re now ready to create a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="abdb2-299">Krok 3.5: Utwórz nowy klucz</span><span class="sxs-lookup"><span data-stu-id="abdb2-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="abdb2-300">Generowanie klucza za pomocą firmy Thales **generatekey** programu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-300">Generate a key by using the Thales **generatekey** program.</span></span>

<span data-ttu-id="abdb2-301">Uruchom następujące polecenie, aby wygenerować klucz:</span><span class="sxs-lookup"><span data-stu-id="abdb2-301">Run the following command to generate the key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="abdb2-302">Po uruchomieniu tego polecenia, użyj tych instrukcji:</span><span class="sxs-lookup"><span data-stu-id="abdb2-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="abdb2-303">Parametr *chronić* musi mieć ustawioną wartość **modułu**, jak pokazano.</span><span class="sxs-lookup"><span data-stu-id="abdb2-303">The parameter *protect* must be set to the value **module**, as shown.</span></span> <span data-ttu-id="abdb2-304">Spowoduje to utworzenie klucza chronionego przez moduł.</span><span class="sxs-lookup"><span data-stu-id="abdb2-304">This creates a module-protected key.</span></span> <span data-ttu-id="abdb2-305">Zestaw narzędzi BYOK nie obsługuje klucze chronione przez OCS.</span><span class="sxs-lookup"><span data-stu-id="abdb2-305">The BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="abdb2-306">Zastąp wartość *contosokey* dla **ident** i **plainname** z dowolną wartością ciągu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-306">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="abdb2-307">Aby zminimalizować ogólne koszty administracyjne i zmniejszyć ryzyko błędów, zaleca się używać tej samej wartości dla obu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-307">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span></span> <span data-ttu-id="abdb2-308">**Ident** wartość musi zawierać tylko cyfry, łączniki i małych liter.</span><span class="sxs-lookup"><span data-stu-id="abdb2-308">The **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="abdb2-309">Parametr pubexp został pozostawiony pusty (wartość domyślna), w tym przykładzie, ale można określić konkretne jego wartości.</span><span class="sxs-lookup"><span data-stu-id="abdb2-309">The pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="abdb2-310">Aby uzyskać więcej informacji zobacz dokumentację firmy Thales.</span><span class="sxs-lookup"><span data-stu-id="abdb2-310">For more information, see the Thales documentation.</span></span>

<span data-ttu-id="abdb2-311">To polecenie tworzy plik Stokenizowanego klucza w folderze %NFAST_KMDATA%\local o nazwach rozpoczynających z **key_simple_**, a następnie **ident** podany w poleceniu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span></span> <span data-ttu-id="abdb2-312">Na przykład: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="abdb2-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="abdb2-313">Ten plik zawiera zaszyfrowany klucz.</span><span class="sxs-lookup"><span data-stu-id="abdb2-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="abdb2-314">Utwórz kopię zapasową tego pliku Stokenizowanego klucza w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="abdb2-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abdb2-315">Po późniejszym przekazaniu klucza do usługi Azure Key Vault, Microsoft nie może wyeksportować tego klucza powrót do tak ważne bezpiecznie kopii zapasowej z klucza oraz środowiska zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="abdb2-315">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="abdb2-316">Skontaktuj się z firmą Thales wskazówki i najlepsze rozwiązania dotyczące tworzenia kopii zapasowej klucza.</span><span class="sxs-lookup"><span data-stu-id="abdb2-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="abdb2-317">Teraz można przystąpić do przenoszenia klucza do usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="abdb2-317">You are now ready to transfer your key to Azure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="abdb2-318">Krok 4: Przygotowanie klucza do przeniesienia</span><span class="sxs-lookup"><span data-stu-id="abdb2-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="abdb2-319">Dla tego czwarty krok wykonaj następujące procedury na odłączonej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="abdb2-319">For this fourth step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="abdb2-320">Krok 4.1: Utwórz kopię klucza z ograniczonymi uprawnieniami</span><span class="sxs-lookup"><span data-stu-id="abdb2-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="abdb2-321">Otwórz nowy wiersz polecenia i zmień bieżący katalog do lokalizacji, w którym unzipped BYOK pliku zip.</span><span class="sxs-lookup"><span data-stu-id="abdb2-321">Open a new command prompt and change the current directory to the location where you unzipped the BYOK zip file.</span></span> <span data-ttu-id="abdb2-322">Aby ograniczyć uprawnienia na klucz, w wierszu polecenia, uruchom jedno z nich, zależnie od regionu geograficznego i wystąpienie usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="abdb2-322">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="abdb2-323">Dla Ameryki Północnej:</span><span class="sxs-lookup"><span data-stu-id="abdb2-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="abdb2-324">Dla Europy:</span><span class="sxs-lookup"><span data-stu-id="abdb2-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="abdb2-325">Dla Azji:</span><span class="sxs-lookup"><span data-stu-id="abdb2-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="abdb2-326">Dla Ameryka Łacińska:</span><span class="sxs-lookup"><span data-stu-id="abdb2-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="abdb2-327">W Japonii:</span><span class="sxs-lookup"><span data-stu-id="abdb2-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="abdb2-328">W przypadku Korei:</span><span class="sxs-lookup"><span data-stu-id="abdb2-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="abdb2-329">Dla Australii:</span><span class="sxs-lookup"><span data-stu-id="abdb2-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="abdb2-330">Aby uzyskać [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych USA Azure:</span><span class="sxs-lookup"><span data-stu-id="abdb2-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="abdb2-331">Dla instytucji rządowych USA DOD:</span><span class="sxs-lookup"><span data-stu-id="abdb2-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="abdb2-332">Dla Kanady:</span><span class="sxs-lookup"><span data-stu-id="abdb2-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="abdb2-333">Niemcy:</span><span class="sxs-lookup"><span data-stu-id="abdb2-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="abdb2-334">Dla Indie:</span><span class="sxs-lookup"><span data-stu-id="abdb2-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="abdb2-335">Podczas uruchamiania tego polecenia Zastąp *contosokey* taką samą wartością jak podana w **3.5 krok: Utwórz nowy klucz** z [generowanie klucza](#step-3-generate-your-key) kroku.</span><span class="sxs-lookup"><span data-stu-id="abdb2-335">When you run this command, replace *contosokey* with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="abdb2-336">Zostanie wyświetlona prośba o podłączenie kart administratora zabezpieczeń world.</span><span class="sxs-lookup"><span data-stu-id="abdb2-336">You are asked to plug in your security world admin cards.</span></span>

<span data-ttu-id="abdb2-337">Po zakończeniu wykonywania polecenia, zostanie wyświetlony **wynik: powodzenie** , a kopia klucza z ograniczonymi uprawnieniami znajdują się w pliku o nazwie key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="abdb2-337">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="abdb2-338">Może przeprowadzający, listy ACL za pomocą następujących poleceń przy użyciu narzędzia firmy Thales:</span><span class="sxs-lookup"><span data-stu-id="abdb2-338">You may inspects the ACLS using following commands using the Thales utilities:</span></span>

* <span data-ttu-id="abdb2-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="abdb2-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="abdb2-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="abdb2-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="abdb2-341">Po uruchomieniu tych poleceń Zastąp contosokey o tej samej wartości określone w **3.5 krok: Utwórz nowy klucz** z [generowanie klucza](#step-3-generate-your-key) kroku.</span><span class="sxs-lookup"><span data-stu-id="abdb2-341">When you run these commands, replace contosokey with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="abdb2-342">Krok 4.2: Zaszyfrowanie klucza przy użyciu klucza wymiany kluczy firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="abdb2-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="abdb2-343">Uruchom jedno z poniższych poleceń, w zależności od Twojego regionu geograficznego lub wystąpienia usługi Azure:</span><span class="sxs-lookup"><span data-stu-id="abdb2-343">Run one of the following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="abdb2-344">Dla Ameryki Północnej:</span><span class="sxs-lookup"><span data-stu-id="abdb2-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-345">Dla Europy:</span><span class="sxs-lookup"><span data-stu-id="abdb2-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-346">Dla Azji:</span><span class="sxs-lookup"><span data-stu-id="abdb2-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-347">Dla Ameryka Łacińska:</span><span class="sxs-lookup"><span data-stu-id="abdb2-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-348">W Japonii:</span><span class="sxs-lookup"><span data-stu-id="abdb2-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-349">W przypadku Korei:</span><span class="sxs-lookup"><span data-stu-id="abdb2-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-350">Dla Australii:</span><span class="sxs-lookup"><span data-stu-id="abdb2-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-351">Aby uzyskać [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych USA Azure:</span><span class="sxs-lookup"><span data-stu-id="abdb2-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-352">Dla instytucji rządowych USA DOD:</span><span class="sxs-lookup"><span data-stu-id="abdb2-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-353">Dla Kanady:</span><span class="sxs-lookup"><span data-stu-id="abdb2-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-354">Niemcy:</span><span class="sxs-lookup"><span data-stu-id="abdb2-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="abdb2-355">Dla Indie:</span><span class="sxs-lookup"><span data-stu-id="abdb2-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="abdb2-356">Po uruchomieniu tego polecenia, użyj tych instrukcji:</span><span class="sxs-lookup"><span data-stu-id="abdb2-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="abdb2-357">Zastąp *contosokey* z identyfikatorem użytym do wygenerowania klucza w **3.5 krok: Utwórz nowy klucz** z [generowanie klucza](#step-3-generate-your-key) kroku.</span><span class="sxs-lookup"><span data-stu-id="abdb2-357">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="abdb2-358">Zastąp *SubscriptionID* z Identyfikatorem subskrypcji Azure, która zawiera magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="abdb2-358">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span></span> <span data-ttu-id="abdb2-359">Tę wartość można pobrać wcześniej w **kroku 1.2: Uzyskaj identyfikator subskrypcji platformy Azure** z [Przygotowanie stacji roboczej podłączonej do Internetu](#step-1-prepare-your-internet-connected-workstation) kroku.</span><span class="sxs-lookup"><span data-stu-id="abdb2-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="abdb2-360">Zastąp *ContosoFirstHSMKey* etykietą, która jest używana do nazwy pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="abdb2-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="abdb2-361">Po pomyślnym zakończeniu, wyświetla **wynik: powodzenie** i ma nowy plik w bieżącym folderze o nazwie następujących: KeyTransferPackage -*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="abdb2-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-to-the-internet-connected-workstation"></a><span data-ttu-id="abdb2-362">Krok 4.3: Skopiowanie pakietu przekazywania klucza do stacji roboczej podłączonej do Internetu</span><span class="sxs-lookup"><span data-stu-id="abdb2-362">Step 4.3: Copy your key transfer package to the Internet-connected workstation</span></span>
<span data-ttu-id="abdb2-363">Aby skopiować plik wyjściowy z poprzedniego kroku (KeyTransferPackage-ContosoFirstHSMkey.byok) do stacji roboczej podłączonej do Internetu, należy użyć dysku USB lub innego przenośnego urządzenia pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="abdb2-363">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-to-azure-key-vault"></a><span data-ttu-id="abdb2-364">Krok 5: Przesłanie klucza do usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="abdb2-364">Step 5: Transfer your key to Azure Key Vault</span></span>
<span data-ttu-id="abdb2-365">W tym kroku końcowego na stacji roboczej podłączonej do Internetu, użyj [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) polecenia cmdlet, aby przekazać pakiet transfer klucza skopiowany z odłączonej stacji roboczej do modułu HSM usługi Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="abdb2-365">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="abdb2-366">Jeśli przekazywanie zakończy się pomyślnie, zostanie wyświetlony wyświetlane właściwości klucza, który właśnie został dodany.</span><span class="sxs-lookup"><span data-stu-id="abdb2-366">If the upload is successful, you see displayed the properties of the key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abdb2-367">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abdb2-367">Next steps</span></span>
<span data-ttu-id="abdb2-368">Można teraz używać tego klucza chronionego przez moduł HSM w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="abdb2-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="abdb2-369">Aby uzyskać więcej informacji, zobacz **Jeśli chcesz użyć sprzętowego modułu zabezpieczeń (HSM)** sekcji [wprowadzenie do korzystania z usługi Azure Key Vault](key-vault-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="abdb2-369">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
