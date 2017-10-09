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
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>Jak toogenerate i przenoszenie kluczy chronionych HSM dla usługi Azure Key Vault
## <a name="introduction"></a>Wprowadzenie
Dla dodatkowego bezpieczeństwa korzystając z usługi Azure Key Vault, można zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM hello. Ten scenariusz jest często określonego tooas *własnego klucza*, byok. Witaj sprzętowych modułów zabezpieczeń są FIPS 140-2 poziom 2 zweryfikowany. Usługa Azure Key Vault używa rodziny nShield firmy Thales tooprotect sprzętowych modułów zabezpieczeń z kluczy.

Użyj informacji hello w tym toohelp temacie Planowanie, generowanie i przekazać swoje własne klucze chronione przez moduł HSM toouse z usługi Azure Key Vault.

Ta funkcja nie jest dostępna dla Chińskiej wersji platformy Azure.

> [!NOTE]
> Aby uzyskać więcej informacji na temat usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](key-vault-whatis.md)  
>
> Pobieranie samouczek Wprowadzenie, łącznie z tworzeniem magazynu kluczy dla kluczy chronionych modułem HSM, zobacz [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).
>
>

Więcej informacji na temat Generowanie i przenoszenie klucza chronionego przez moduł HSM za pośrednictwem Internetu hello:

* W trybie offline stację roboczą, co zmniejsza możliwości ataku hello jest generowanie klucza hello.
* klucz Hello jest szyfrowany z klucza wymiany klucza (KEK), który pozostaje zaszyfrowany, dopóki nie zostanie przeniesione toohello modułów HSM usługi Azure Key Vault. Tylko hello zaszyfrowana wersja klucza opuszcza pierwotną stację roboczą hello.
* zestaw narzędzi Hello ustawia właściwości klucz dzierżawy, który wiąże się z klucza toohello środowiska zabezpieczeń security world usługi Azure Key Vault. Dlatego po hello modułów HSM usługi Azure Key Vault odbiorą i odszyfrują klucz, tylko te moduły HSM może być używany. Nie można wyeksportować klucza. To powiązanie jest wymuszone przez hello sprzętowych modułów zabezpieczeń firmy Thales.
* Witaj klucza wymiany klucza (KEK), który jest używany tooencrypt klucz jest generowany wewnątrz hello modułów HSM usługi Azure Key Vault i nie jest możliwy do eksportu. Moduły HSM Hello wymusić nie był dostępny nie ma wersji wyczyść hello KEK poza hello sprzętowych modułów zabezpieczeń. Ponadto hello zestaw narzędzi zawiera zaświadczenie od firmy Thales tego hello KEK nie można wyeksportować i został wygenerowany w oryginalnym module HSM, który wyprodukowanego przez firmę Thales.
* Witaj zestaw narzędzi zawiera zaświadczenie od firmy Thales tego hello Azure Key Vault środowiska zabezpieczeń security world zostało także wygenerowane w oryginalnym sprzętowym module zabezpieczeń wyprodukowanym przez firmę Thales. To poświadczenie okaże się tooyou, że firma Microsoft korzysta z oryginalnego sprzętu.
* Firma Microsoft używa oddzielnych kluczy Kek i oddzielne środowiska Security World w każdym regionie geograficznym. Ta separacja gwarantuje, że klucz może służyć wyłącznie w centrach danych w regionie hello, w którym został zaszyfrowany. Na przykład klucz Europejskiego klienta nie można użyć w centrach danych w Ameryce Północnej ani Azji.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Więcej informacji na temat sprzętowych modułów zabezpieczeń firmy Thales i usług firmy Microsoft
Firmy Thales e-Security jest wiodącym globalnym dostawcą szyfrowania danych i usług finansowych toohello rozwiązań zabezpieczeń przez, zaawansowanych technologii, produkcyjnym, dla instytucji rządowych i sektorów technologii. 40 lat udokumentowanego doświadczenia ochrony firmy i informacje dla instytucji rządowych rozwiązania firmy Thales są używane przez cztery hello pięć największe energii i aerospace firmy. Ich rozwiązania są również używane przez 22 kraje NATO, a secure ponad 80 procent transakcji płatniczych na świecie.

Firma Microsoft podjęła współpracę ze stanem hello tooenhance firmy Thales wiedzę w zakresie sprzętowych modułów zabezpieczeń. Te ulepszenia umożliwiają tooget hello typowych zalet usług hostowanych bez potrzeby rezygnacji z kontroli nad kluczami. W szczególności ulepszenia te umożliwiają firmie Microsoft Zarządzanie hello sprzętowych modułów zabezpieczeń, dzięki czemu nie trzeba. Jako chmury usługi, usługi Azure Key Vault skaluje w krótkim czasie toomeet wzrósł użytkowania Twojej organizacji. At hello sam czasu klucz jest chroniony wewnątrz sprzętowych modułów zabezpieczeń firmy Microsoft: użytkownik zachowuje kontrolę nad hello cyklu życia klucza, ponieważ generowanie klucza hello i przenieść na tooMicrosoft sprzętowych modułów zabezpieczeń.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Implementowanie Użyj własnego klucza (BYOK) dla usługi Azure Key Vault
Użyj hello następujące informacje i procedury, jeśli będzie generowanie własnego klucza chronionego przez moduł HSM, a następnie przenieść je tooAzure Key Vault — Witaj Przełącz scenariusz klucza (BYOK).

## <a name="prerequisites-for-byok"></a>Wymagania wstępne dotyczące funkcji BYOK
Zobacz hello w poniższej tabeli, aby uzyskać listę wymagań wstępnych dotyczących Użyj własnego klucza (BYOK) dla usługi Azure Key Vault.

| Wymaganie | Więcej informacji |
| --- | --- |
| TooAzure subskrypcji |toocreate usługi Azure Key Vault, potrzebujesz subskrypcji platformy Azure: [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/) |
| Witaj kluczy chronionego przez moduł HSM toosupport warstwy usługi Azure klucza magazynu w warstwie Premium |Aby uzyskać więcej informacji o hello warstwy usług i możliwości usługi Azure Key Vault, zobacz hello [cennik usługi Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) witryny sieci Web. |
| Modułu HSM firmy Thales, karty inteligentne i oprogramowanie |Musi mieć dostęp do tooa sprzętowego modułu zabezpieczeń firmy Thales i podstawowe wiedzę na temat działania sprzętowych modułów zabezpieczeń firmy Thales. Zobacz [sprzętowego modułu zabezpieczeń firmy Thales](https://www.thales-esecurity.com/msrms/buy) hello lista zgodnych modeli lub toopurchase modułu HSM, jeśli nie istnieje. |
| Witaj następujący sprzęt i oprogramowanie:<ol><li>W trybie offline x64 stacja robocza z systemem operacyjnym Windows z systemem Windows 7 oraz oprogramowaniem Thales nShield w wersji 11.50.<br/><br/>Jeśli stacja robocza z systemem Windows 7, należy najpierw [instalacja programu Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</li><li>Stacja robocza toohello połączenia internetowego i ma system operacyjny Windows Windows 7 i [programu Azure PowerShell](/powershell/azure/overview) **minimalna wersja 1.1.0** zainstalowane.</li><li>Dysk USB lub inne przenośne urządzenie pamięci masowej z co najmniej 16 MB wolnego miejsca.</li></ol> |Ze względów bezpieczeństwa zaleca się pierwsza stacja robocza tego hello nie jest połączony tooa sieci. Jednak to zalecenie nie jest programowo wymuszana.<br/><br/>Należy pamiętać, że w postępuj zgodnie z instrukcjami hello tej stacji roboczej stacji roboczej hello odłączony tooas określony.</p></blockquote><br/>Ponadto jeśli klucz dzierżawy jest przeznaczony dla środowiska produkcyjnego, zaleca się użycie drugiej, oddzielnej stacji roboczej toodownload hello zestaw narzędzi i przekazywanie hello klucz dzierżawy. Do celów testowych można używać hello stacji roboczej, jako hello pierwsza z nich.<br/><br/>Należy pamiętać, że w postępuj zgodnie z instrukcjami hello druga stacja robocza stacji roboczej określonego tooas hello podłączonej do Internetu.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>Generowanie i przenoszenie z tooAzure klucza HSM magazyn kluczy
Będą używać hello następujące pięć toogenerate kroki i transfer Twojego klucza tooan modułu HSM usługi Azure Key Vault:

* [Krok 1: Przygotowanie stacji roboczej podłączonej do Internetu](#step-1-prepare-your-internet-connected-workstation)
* [Krok 2: Przygotowanie odłączonej stacji roboczej](#step-2-prepare-your-disconnected-workstation)
* [Krok 3: Generowanie klucza](#step-3-generate-your-key)
* [Krok 4: Przygotowanie klucza do przeniesienia](#step-4-prepare-your-key-for-transfer)
* [Krok 5: Transfer z tooAzure klucza Key Vault](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>Krok 1: Przygotowanie stacji roboczej podłączonej do Internetu
W tym kroku pierwszego hello procedur przedstawionych na stacji roboczej, który jest połączony toohello Internet.

### <a name="step-11-install-azure-powershell"></a>Krok 1.1: Instalowanie programu Azure PowerShell
Stacji roboczej podłączonej do Internetu hello Pobierz i zainstaluj hello modułu Azure PowerShell, która obejmuje hello toomanage poleceń cmdlet usługi Azure Key Vault. Wymaga minimalnej wersji 0.8.13.

Aby uzyskać instrukcje instalacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

### <a name="step-12-get-your-azure-subscription-id"></a>Krok 1.2: Pobieranie identyfikator subskrypcji platformy Azure
Uruchom sesję programu PowerShell Azure i zaloguj się przy użyciu następującego polecenia hello tooyour konto platformy Azure:

        Add-AzureAccount
W oknie wyskakującym przeglądarki hello wprowadź nazwę użytkownika konta platformy Azure i hasło. Następnie należy użyć hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) polecenia:

        Get-AzureSubscription
Z danych wyjściowych hello zlokalizuj identyfikator hello hello subskrypcji, które będą używane dla usługi Azure Key Vault. Ta Subskrypcja będzie potrzebny później.

Nie zamykaj okna programu Azure PowerShell hello.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>Krok 1.3: Pobierz hello zestawu narzędzi BYOK dla usługi Azure Key Vault
Przejdź toohello Microsoft Download Center i [pobrania zestawu narzędzi BYOK magazynu kluczy Azure hello](http://www.microsoft.com/download/details.aspx?id=45345) regionu geograficznego lub wystąpienia platformy Azure. Witaj poniższych informacji tooidentify hello pakietu Nazwa toodownload i jego odpowiedniego algorytmu SHA-256 pakietu wyznaczania wartości skrótu:

- - -
**Stany Zjednoczone:**

States.zip KeyVault-BYOK-Tools Zjednoczone

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**Europa:**

KeyVault-BYOK-Tools-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**Azja:**

KeyVault-BYOK-Tools-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**Ameryka Łacińska:**

KeyVault-BYOK-Tools-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**Japonia:**

KeyVault-BYOK-Tools-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**Korea:**

KeyVault-BYOK-Tools-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**Australia:**

KeyVault-BYOK-Tools-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure dla instytucji rządowych:**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-Tools-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**Dla instytucji rządowych USA DOD:**

KeyVault-BYOK-Tools-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**Kanada:**

KeyVault-BYOK-Tools-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**Niemcy:**

KeyVault-BYOK-Tools-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**Indie:**

KeyVault-BYOK-Tools-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**Wielka Brytania:**

KeyVault-BYOK-Tools-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

integralność hello toovalidate Twojego pobranego zestawu narzędzi BYOK, w sesji programu Azure PowerShell, użyj hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) polecenia cmdlet.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

Witaj zestaw narzędzi zawiera następujące hello:

* Pakiet klucza wymiany klucza (KEK), którego nazwa zaczyna się od **BYOK-KEK - pkg-.**
* Pakiet środowiska zabezpieczeń Security World, którego nazwa zaczyna się od **BYOK-SecurityWorld - pkg-.**
* Skrypt w języku python o nazwie **verifykeypackage.py.**
* Plik wykonywalny wiersza polecenia o nazwie **KeyTransferRemote.exe** oraz skojarzone biblioteki dll.
* Pakiet redystrybucyjny Visual C++, o nazwie **vcredist_x64.exe.**

Kopiuj hello pakietu tooa USB lub innego przenośnego urządzenia pamięci masowej.

## <a name="step-2-prepare-your-disconnected-workstation"></a>Krok 2: Przygotowanie odłączonej stacji roboczej
W tym kroku drugi hello procedur przedstawionych na powitania stacji roboczej, która nie jest siecią połączonych tooa (hello Internetu lub sieci wewnętrznej).

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>Krok 2.1: Przygotowanie stacji roboczej hello odłączony z modułu HSM firmy Thales
Zainstaluj oprogramowanie wspomagające nCipher (firmy Thales) hello na komputerze z systemem Windows, a następnie dołącz komputer toothat modułu HSM firmy Thales.

Upewnij się, że hello narzędzia firmy Thales znajdują się w ścieżce (**%nfast_home%\bin**). Na przykład wpisz następujące hello:

        set PATH=%PATH%;"%nfast_home%\bin"

Aby uzyskać więcej informacji zobacz Podręcznik użytkownika hello dołączonego hello modułu HSM firmy Thales.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>Krok 2.2: Zestaw narzędzi BYOK hello instalacji hello odłączony stacji roboczej
Skopiuj pakiet zestawu narzędzi BYOK hello hello dysk USB lub innego przenośnego urządzenia pamięci masowej, a następnie hello następujące:

1. Wyodrębnij pliki hello z pakietu hello pobrane do dowolnego folderu.
2. Uruchom program vcredist_x64.exe z tego folderu.
3. Postępuj zgodnie z instrukcjami hello toohello instalują elementy środowiska uruchomieniowego Visual C++ hello for Visual Studio 2013.

## <a name="step-3-generate-your-key"></a>Krok 3: Generowanie klucza
W tym kroku trzeci hello procedur przedstawionych na stacji roboczej hello odłączony. toocomplete ten krok modułu HSM musi być w trybie inicjowania. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>Krok 3.1: Zmień hello HSM tryb too'I "
Jeśli używasz nShield firmy Thales krawędzi, tryb hello toochange: 1. W trybie hello tryb przycisku toohighlight hello wymagane. 2. W ciągu kilku sekund naciśnij i przytrzymaj ją przycisk Wyczyść hello kilka sekund. W przypadku zmiany trybu hello, hello LED nowy tryb zatrzymuje miga i pozostaje podświetlone. Hello LED stanu może flash nieregularnych przez kilka sekund i następnie miga regularnie, gdy urządzenie hello jest gotowe. W przeciwnym razie hello urządzenie pozostaje w bieżącym trybie hello z hello odpowiedni tryb LED włączone.

### <a name="step-32-create-a-security-world"></a>Krok 3.2: Utworzenie środowiska zabezpieczeń security world
Uruchom wiersz polecenia i uruchom hello program nowe world firmy Thales.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

Ten program tworzy **środowiska zabezpieczeń Security World** pliku w lokalizacji % NFAST_KMDATA%\local\world, co odpowiada toohello folderu C:\ProgramData\nCipher\Key Management Data\local. Można użyć innych wartości dla kworum hello, ale w tym przykładzie użytkownik ma tooenter zostanie wyświetlony monit o trzech pustych kart oraz kodów PIN dla każdego z nich. Następnie dowolne dwie spośród kart nadaj środowiska zabezpieczeń security world toohello pełny dostęp. Te karty stają się hello **zestaw kart administratora** dla hello nowego środowiska zabezpieczeń.

Następnie hello następujące:

* Utwórz kopię zapasową hello world pliku. Zabezpieczenia ochrony hello world pliku, hello kart administratora i numerów PIN i upewnij się, że nikt ma toomore dostępu niż jedną kartę.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>Krok 3.3: Zmień hello HSM tryb too'O "
Jeśli używasz nShield firmy Thales krawędzi, tryb hello toochange: 1. W trybie hello tryb przycisku toohighlight hello wymagane. 2. W ciągu kilku sekund naciśnij i przytrzymaj ją przycisk Wyczyść hello kilka sekund. W przypadku zmiany trybu hello, hello LED nowy tryb zatrzymuje miga i pozostaje podświetlone. Hello LED stanu może flash nieregularnych przez kilka sekund i następnie miga regularnie, gdy urządzenie hello jest gotowe. W przeciwnym razie hello urządzenie pozostaje w bieżącym trybie hello z hello odpowiedni tryb LED włączone.


### <a name="step-34-validate-hello-downloaded-package"></a>Krok 3.4: Sprawdzanie poprawności pakietu hello pobrane
Ten krok jest opcjonalny, ale zalecany, dzięki czemu można zweryfikować następujących hello:

* Hello klucz wymiany klucza jest uwzględniona w hello narzędzi został wygenerowany w oryginalnym module HSM firmy Thales.
* Skrót Hello hello World zabezpieczeń, uwzględnionej w hello narzędzi został wygenerowany w oryginalnym module HSM firmy Thales.
* Klucz wymiany klucza Hello jest nie może zostać wyeksportowany.

> [!NOTE]
> Witaj toovalidate pobrano pakiet, hello HSM musi być podłączony, włączona i musi mieć zabezpieczeń security world na nim (na przykład hello jedną właśnie utworzone).
>
>

Pakiet pobrany hello toovalidate:

1. Uruchom skrypt verifykeypackage.py hello wpisując jedną z następujących hello, zależnie od regionu geograficznego i wystąpienia platformy Azure:

   * Dla Ameryki Północnej:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * Dla Europy:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * Dla Azji:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * Dla Ameryka Łacińska:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * W Japonii:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * W przypadku Korei:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * Dla Australii:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * Dla [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych hello USA Azure:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * Dla instytucji rządowych USA DOD:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * Dla Kanady:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * Niemcy:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * Dla Indie:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > Witaj oprogramowanie firmy Thales obejmuje python w %NFAST_HOME%\python\bin
     >
     >
2. Upewnij się, zobacz temat hello następujący komunikat, który wskazuje pomyślnym zweryfikowaniem: **wynik: powodzenie**

Ten skrypt sprawdza łańcuch osoby podpisującej hello się toohello klucza głównego firmy Thales. Hello skrót klucza głównego jest osadzony w skrypcie hello i jego wartość powinna wynosić **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Można również potwierdzić tę wartość osobno, odwiedzając hello [witryny sieci Web firmy Thales](http://www.thalesesec.com/).

Możesz teraz gotowy toocreate nowy klucz.

### <a name="step-35-create-a-new-key"></a>Krok 3.5: Utwórz nowy klucz
Generowanie klucza za pomocą hello firmy Thales **generatekey** programu.

Uruchom powitania po klucz hello toogenerate polecenia:

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

Po uruchomieniu tego polecenia, użyj tych instrukcji:

* Witaj parametru *chronić* należy ustawić wartość toohello **modułu**, jak pokazano. Spowoduje to utworzenie klucza chronionego przez moduł. Witaj zestawu narzędzi BYOK nie obsługuje klucze chronione przez OCS.
* Zastąp wartość hello *contosokey* dla hello **ident** i **plainname** z dowolną wartością ciągu. toominimize ogólne koszty administracyjne i zmniejszyć ryzyko hello błędów, zalecane jest użycie hello samą wartość dla obu. Witaj **ident** wartość musi zawierać tylko cyfry, łączniki i małych liter.
* Parametr Hello pubexp został pozostawiony pusty (wartość domyślna), w tym przykładzie, ale można określić konkretne jego wartości. Aby uzyskać więcej informacji, zobacz hello dokumentacji firmy Thales.

To polecenie tworzy plik Stokenizowanego klucza w folderze %NFAST_KMDATA%\local o nazwach rozpoczynających z **key_simple_**, a następnie hello **ident** podany w poleceniu hello. Na przykład: **key_simple_contosokey**. Ten plik zawiera zaszyfrowany klucz.

Utwórz kopię zapasową tego pliku Stokenizowanego klucza w bezpiecznym miejscu.

> [!IMPORTANT]
> Po późniejszym przekazaniu Twojej tooAzure klucza Key Vault, Microsoft nie może wyeksportować tego klucza zapasowego tooyou tak ważne bezpiecznie kopii zapasowej z klucza oraz środowiska zabezpieczeń. Skontaktuj się z firmą Thales wskazówki i najlepsze rozwiązania dotyczące tworzenia kopii zapasowej klucza.
>
>

Możesz są teraz gotowe tootransfer Twojego klucza tooAzure magazynu kluczy.

## <a name="step-4-prepare-your-key-for-transfer"></a>Krok 4: Przygotowanie klucza do przeniesienia
W tym kroku czwarty hello procedur przedstawionych na stacji roboczej hello odłączony.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>Krok 4.1: Utwórz kopię klucza z ograniczonymi uprawnieniami

Otwórz nowy wiersz polecenia i zmień hello bieżącego katalogu toohello lokalizację gdzie można rozpakować pliku zip BYOK hello. uprawnienia hello tooreduce na klucz, w wierszu polecenia Uruchom jedno z następujących hello, zależnie od regionu geograficznego i wystąpienie usługi Azure:

* Dla Ameryki Północnej:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* Dla Europy:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* Dla Azji:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* Dla Ameryka Łacińska:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* W Japonii:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* W przypadku Korei:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* Dla Australii:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* Dla [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych hello USA Azure:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* Dla instytucji rządowych USA DOD:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* Dla Kanady:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* Niemcy:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* Dla Indie:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

Podczas uruchamiania tego polecenia Zastąp *contosokey* z hello samą wartość podana w **3.5 krok: Utwórz nowy klucz** z hello [generowanie klucza](#step-3-generate-your-key) kroku.

Zostanie wyświetlona prośba tooplug w world kart administratora zabezpieczeń.

Gdy hello zakończeniu wykonywania polecenia zostanie wyświetlony **wynik: powodzenie** i hello kopii klucza z ograniczonymi uprawnieniami znajdują się w pliku hello o nazwie key_xferacId_<contosokey>.

Może przeprowadzający hello listy ACL za pomocą następujących poleceń przy użyciu hello narzędzia firmy Thales:

* aclprint.py:

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe:

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  Po uruchomieniu tych poleceń Zastąp contosokey hello samą wartość podana w **3.5 krok: Utwórz nowy klucz** z hello [generowanie klucza](#step-3-generate-your-key) kroku.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>Krok 4.2: Zaszyfrowanie klucza przy użyciu klucza wymiany kluczy firmy Microsoft
Uruchom jedno z hello następujące polecenia, zależnie od regionu geograficznego i wystąpienie usługi Azure:

* Dla Ameryki Północnej:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Dla Europy:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Dla Azji:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Dla Ameryka Łacińska:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* W Japonii:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* W przypadku Korei:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Dla Australii:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Dla [Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/), który używa wystąpienia dla instytucji rządowych hello USA Azure:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Dla instytucji rządowych USA DOD:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Dla Kanady:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Niemcy:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Dla Indie:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

Po uruchomieniu tego polecenia, użyj tych instrukcji:

* Zastąp *contosokey* używany klucz hello toogenerate w identyfikatorze hello **3.5 krok: Utwórz nowy klucz** z hello [generowanie klucza](#step-3-generate-your-key) kroku.
* Zastąp *SubscriptionID* o identyfikatorze hello hello subskrypcji Azure, która zawiera magazynu kluczy. Tę wartość można pobrać wcześniej w **kroku 1.2: Uzyskaj identyfikator subskrypcji platformy Azure** z hello [Przygotowanie stacji roboczej podłączonej do Internetu](#step-1-prepare-your-internet-connected-workstation) krok.
* Zastąp *ContosoFirstHSMKey* etykietą, która jest używana do nazwy pliku wyjściowego.

Po pomyślnym zakończeniu, wyświetla **wynik: powodzenie** i ma nowy plik w folderze bieżącego hello, który ma hello następującej nazwie: KeyTransferPackage -*ContosoFirstHSMkey*.byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>Krok 4.3: Przekazanie klucza pakietu toohello połączony z Internetem stacji roboczej do kopiowania
Użyj dysku USB lub innego przenośnego urządzenia pamięci masowej toocopy hello wyjściowego pliku hello poprzedniego kroku (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour połączony z Internetem stacji roboczej.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>Krok 5: Transfer z tooAzure klucza Key Vault
Ten ostatni krok na stacji roboczej podłączonej do Internetu hello, użyć hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) pakietu przekazywania klucza hello tooupload polecenia cmdlet, skopiowany z hello odłączony toohello stacji roboczej modułu HSM usługi Azure Key Vault:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Jeśli przekazywanie hello zakończy się pomyślnie, zobaczysz właściwości wyświetlane hello hello klucza, który właśnie został dodany.

## <a name="next-steps"></a>Następne kroki
Można teraz używać tego klucza chronionego przez moduł HSM w magazynie kluczy. Aby uzyskać więcej informacji, zobacz hello **Jeśli chcesz toouse sprzętowego modułu zabezpieczeń (HSM)** części hello [wprowadzenie do korzystania z usługi Azure Key Vault](key-vault-get-started.md) samouczka.
