---
title: "aaaGet wprowadzenie do usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka toohelp otrzymasz wprowadzenie do usługi Azure Key Vault toocreate wzmocnionego kontenera na platformie Azure, toostore i zarządzanie nimi kluczy kryptograficznych i kluczy tajnych na platformie Azure."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Rozpoczynanie pracy z usługą Azure Key Vault
Usługa Azure Key Vault jest dostępna w większości regionów. Aby uzyskać więcej informacji, zobacz hello [cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Wprowadzenie
Użyj tego samouczka toohelp otrzymasz wprowadzenie do usługi Azure Key Vault toocreate wzmocnionego kontenera (magazynu) na platformie Azure, toostore i zarządzanie nimi kluczy kryptograficznych i kluczy tajnych na platformie Azure. Przeprowadza użytkownika przez proces hello przy użyciu programu Azure PowerShell toocreate magazynu, który zawiera klucz lub hasło, które następnie można za pomocą aplikacji Azure. Następnie pokaże Ci, w jaki sposób aplikacja może użyć tego klucza lub hasła.

**Szacowany czas toocomplete:** 20 minut

> [!NOTE]
> Ten samouczek nie zawiera instrukcje dotyczące sposobu hello toowrite aplikacji Azure, która zawiera jeden z kroków hello, czyli jak tooauthorize toouse aplikacji klucza lub klucza tajnego klucza hello magazynu.
>
> W tym samouczku jest używany program Azure PowerShell. Instrukcje dotyczące wieloplatformowego interfejsu wiersza polecenia znajdują się w [tym równoważnym samouczku](key-vault-manage-with-cli2.md).
>
>

Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka, musi mieć następujące hello:

* TooMicrosoft subskrypcji Azure. Jeśli jej nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/pricing/free-trial/).
* Program Azure PowerShell, **minimalna wersja 1.1.0**. tooinstall programu Azure PowerShell i skojarzyć go z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Jeśli jest już zainstalowany program Azure PowerShell, a nie znasz wersji hello z konsoli programu Azure PowerShell hello, wpisz `(Get-Module azure -ListAvailable).Version`. Jeśli masz zainstalowany program Azure PowerShell w wersji od 0.9.1 do 0.9.8, nadal możesz korzystać tego samouczka z niewielkimi zmianami. Na przykład, należy użyć hello `Switch-AzureMode AzureResourceManager` polecenia i niektórych poleceń usługi Azure Key Vault hello zostały zmienione. Aby uzyskać listę hello poleceń cmdlet usługi Key Vault dla wersji od 0.9.1 do 0.9.8, zobacz [polecenia cmdlet usługi Azure Key Vault](/powershell/module/azurerm.keyvault/#key_vault).
* Aplikacja, która będzie skonfigurowany toouse hello klucza lub hasła utworzonego w ramach tego samouczka. Przykładowa aplikacja jest dostępna z hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343). Aby uzyskać instrukcje Zobacz hello towarzyszący plik Readme.

Ten samouczek jest przeznaczony dla początkujących użytkowników programu Azure PowerShell, ale przyjęto założenie, że rozumiesz podstawowe pojęcia hello, takie jak moduły, polecenia cmdlet i sesje. Aby uzyskać więcej informacji, zobacz artykuł [Wprowadzenie do programu Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).

tooget szczegółową pomoc dla każdego polecenia cmdlet, które pojawi się w tym samouczku, użyj hello **Get-Help** polecenia cmdlet.

    Get-Help <cmdlet-name> -Detailed

Na przykład tooget pomocy hello **Login-AzureRmAccount** polecenia cmdlet, wpisz:

    Get-Help Login-AzureRmAccount -Detailed

Możesz przeczytać następujące samouczki tooget zapoznać się z usługą Azure Resource Manager w programie Azure PowerShell hello:

* [Jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview)
* [Używanie programu Azure PowerShell z usługą Resource Manager](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Połącz tooyour subskrypcji
Uruchom sesję programu PowerShell Azure i zaloguj się tooyour konto platformy Azure za pomocą następującego polecenia hello:  

    Login-AzureRmAccount

Należy pamiętać, że jeśli używasz konkretnego wystąpienia platformy Azure, na przykład Azure dla instytucji rządowych, użyj hello - parametru środowiska za pomocą tego polecenia. Na przykład: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

W oknie wyskakującym przeglądarki hello wprowadź nazwę użytkownika konta platformy Azure i hasło. Program Azure PowerShell pobiera wszystkie subskrypcje hello, które są skojarzone z tym kontem i domyślnie, używa hello pierwsza z nich.

Jeśli masz wiele subskrypcji i chcesz toospecify określonych toouse jeden dla usługi Azure Key Vault, wpisz powitania po toosee hello subskrypcje dla swojego konta:

    Get-AzureRmSubscription

Następnie toospecify hello subskrypcji toouse, wpisz:

    Set-AzureRmContext -SubscriptionId <subscription ID>

Aby uzyskać więcej informacji na temat konfigurowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a id="resource"></a>Tworzenie nowej grupy zasobów
Podczas korzystania z usługi Azure Resource Manager wszystkie powiązane zasoby są tworzone wewnątrz grupy zasobów. W tym samouczku utworzysz nową grupę zasobów o nazwie **ContosoResourceGroup**:

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>Tworzenie magazynu kluczy
Użyj hello [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) toocreate polecenia cmdlet magazynu kluczy. To polecenie cmdlet ma trzy obowiązkowe parametry: **Nazwa grupy zasobów**, **nazwa magazynu kluczy**i hello **lokalizacji geograficznej**.

Na przykład, jeśli używasz nazwy magazynu hello **ContosoKeyVault**, nazwę grupy zasobów hello **ContosoResourceGroup**i lokalizację hello **Azja Wschodnia**, typ:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

Hello wyjściem tego polecenia cmdlet pokazują właściwości magazynu kluczy hello nowo utworzony. Witaj dwie najważniejsze właściwości to:

* **Nazwa magazynu**: W przykładzie hello jest **ContosoKeyVault**. Ta nazwa będzie używana do innych poleceń cmdlet usługi Key Vault.
* **Identyfikator URI magazynu**: W przykładzie hello jest to https://contosokeyvault.vault.azure.net/. Aplikacje korzystające z magazynu za pomocą jego interfejsu API REST muszą używać tego identyfikatora URI.

Konto platformy Azure jest teraz autoryzowanych tooperform żadnych operacji dla tego klucza magazynu. Nikt inny nie jest do tego upoważniony.

> [!NOTE]
> Jeśli zostanie wyświetlony błąd hello **hello subskrypcja nie jest zarejestrowany toouse przestrzeni nazw "Microsoft.KeyVault"** podczas toocreate nowego magazynu kluczy, uruchom `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` , a następnie uruchom ponownie polecenie New-AzureRmKeyVault. Aby uzyskać więcej informacji, zobacz temat [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).
>
>

## <a id="add"></a>Dodawanie klucza lub magazynu kluczy tajnych toohello
Usługa Azure Key Vault toocreate klucza chronionego przez oprogramowanie dla Ciebie, należy użyć hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) polecenia cmdlet i wpisz następujące hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

Jednak jeśli masz istniejący klucz chroniony oprogramowaniem. Tooyour zapisać plik PFX C:\ na dysku w pliku o nazwie softkey.pfx, które mają tooAzure tooupload Key Vault hello typu następującej zmiennej hello tooset **securepfxpwd** na hasło **123** dla hello. Plik PFX:

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

Następnie wpisz powitania po klucz hello tooimport z hello. Plik PFX, który chroni klucz hello przez oprogramowanie w usłudze Key Vault hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


Teraz możesz odwoływać ten klucz został utworzony lub przekazany tooAzure Key Vault, za pomocą jego identyfikatora URI. Użyj **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways uzyskać hello bieżącą wersję oraz **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tę konkretną wersję.  

Witaj toodisplay identyfikatora URI dla tego klucza, wpisz:

    $Key.key.kid

tooadd magazynu toohello tajny, który jest hasłem o nazwie SQLPassword i ma wartość Pa$ $w0rd tooAzure Key Vault hello, najpierw przekonwertuj wartość Pa$ $w0rd tooa bezpieczny ciąg hello, wpisując następujące hello:

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

Następnie wpisz następujące hello:

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

Teraz możesz odwoływać się to hasło, dodać tooAzure Key Vault, za pomocą jego identyfikatora URI. Użyj **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways uzyskać hello bieżącą wersję oraz **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tę konkretną wersję.

Witaj toodisplay identyfikatora URI dla tego klucza tajnego, wpisz:

    $secret.Id

Teraz wyświetlić hello klucz lub klucz tajny, który został właśnie utworzony:

* tooview Twojego klucza, wpisz:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview tajne, typu:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

Teraz Twojego magazynu kluczy oraz klucz lub klucz tajny jest gotowy do toouse aplikacji. Musisz zezwolić aplikacji toouse je.  

## <a id="register"></a>Rejestrowanie aplikacji w usłudze Azure Active Directory
Ten krok będzie zazwyczaj wykonywany przez programistę na innym komputerze. Nie jest określonym tooAzure Key Vault, ale został tu zawarty, aby informacje były kompletne.

> [!IMPORTANT]
> toocomplete hello samouczek, Twoje konto, Magazyn hello i aplikacji hello, która zarejestruje się w tym kroku musi być w hello tego samego katalogu Azure.
>
>

Aplikacje używające magazynu kluczy muszą zostać uwierzytelnione przy użyciu tokenu z usługi Azure Active Directory. toodo hello, właściciel aplikacji hello aplikacji hello najpierw należy zarejestrować w usłudze Azure Active Directory. Na powitania koniec rejestracji właściciel aplikacji hello pobiera hello następujące wartości:

* **Identyfikator aplikacji** (znanej także jako identyfikator klienta) i **klucz uwierzytelniania** (znanej także jako hello wspólny klucz tajny). Witaj, aplikacja musi przedstawić obie te wartości tooAzure usługi Active Directory, tooget tokenu. Jak aplikacja hello jest skonfigurowany toodo, który zależy od aplikacji hello. Dla usługi Key Vault Przykładowa aplikacja hello hello właściciel aplikacji ustawia te wartości w pliku app.config hello.

Aplikacja hello tooregister w usłudze Azure Active Directory:

1. Zaloguj się toohello klasycznego portalu Azure.
2. Powitania po lewej stronie, kliknij przycisk **usługi Active Directory**, a następnie wybierz katalog hello, w którym będzie rejestrować aplikacji. <br> <br> **Uwaga:** należy wybrać hello tym samym katalogu, który zawiera hello subskrypcji platformy Azure, z którym zostanie utworzony magazyn kluczy. Jeśli nie znasz katalog ten jest, kliknij przycisk **ustawienia**zidentyfikować hello subskrypcji, z którym zostanie utworzony magazyn kluczy i w ostatniej kolumnie hello wyświetlana nazwa hello Uwaga hello katalogu.
3. Kliknij pozycję **APLIKACJE**. Jeśli nie aplikacja nie została dodana tooyour katalogu, tej stronie są wyświetlane tylko hello **Dodaj aplikację** łącza. Kliknij łącze hello lub Alternatywnie możesz kliknąć **dodać** na powitania paska poleceń.
4. W hello **Dodawanie aplikacji** kreatora, na powitania **co chcesz toodo?** kliknij przycisk **Dodaj aplikację moją organizację**.
5. Na powitania **Powiedz nam o aplikacji** strony, określ nazwę aplikacji, a następnie wybierz **interfejsu API sieci WEB i/lub aplikacji sieci WEB** (hello domyślną). Kliknij przycisk hello **dalej** ikony.
6. Na powitania **właściwości aplikacji** Określ hello **adres URL logowania** i **identyfikator URI aplikacji** dla aplikacji sieci web. Jeśli aplikacja nie ma tych wartości, możesz je wymyślić na potrzeby tego kroku (na przykład możesz wpisać adres http://test1.contoso.com w obu polach). Nie ma znaczenia, czy takie witryny istnieją. Ważne jest, aplikacja hello identyfikator URI dla każdej aplikacji jest różne dla każdej aplikacji w katalogu. katalog Hello używa tego ciągu tooidentify aplikacji.
7. Kliknij przycisk hello **Complete** toosave ikona zmiany w Kreatorze hello.
8. Na powitania **Szybki Start** kliknij przycisk **Konfiguruj**.
9. Przewiń toohello **klucze** sekcji, wybierz czas trwania hello, a następnie kliknij przycisk **ZAPISAĆ**. Strona Hello odświeżona i pojawi się wartość klucza. Należy skonfigurować aplikację za pomocą wartości klucza i hello **identyfikator klienta** wartość. (Instrukcje dotyczące tej konfiguracji są specyficzne dla aplikacji).
10. Skopiuj wartość Identyfikatora powitania klienta z tej strony, który będzie używany w hello następny krok tooset uprawnień dotyczących magazynu.

## <a id="authorize"></a>Autoryzowanie hello aplikacji toouse hello klucza lub klucza tajnego
Witaj tooaccess aplikacji hello tooauthorize klucza lub klucza tajnego w magazynie hello, użyj [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) polecenia cmdlet.

Na przykład, jeśli nazwa Twojego magazynu to **ContosoKeyVault** i tooauthorize ma identyfikator klienta 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed i ma toodecrypt aplikacji hello tooauthorize i zaloguj się za pomocą kluczy w aplikacji hello magazynie, uruchom następujące hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Jeśli chcesz tooauthorize tego samego hasła tooread aplikacji w magazynie, uruchom następujące hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>Jeśli chcesz, aby toouse sprzętowego modułu zabezpieczeń (HSM)
Dla dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM hello. Witaj sprzętowych modułów zabezpieczeń są FIPS 140-2 poziom 2 zweryfikowany. Jeśli te wymagania nie odnoszą się tooyou, Pomiń tę sekcję i przejdź zbyt[usunąć hello magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych](#delete).

toocreate klucze chronionego przez moduł HSM, należy użyć hello [klucze chronione przez moduł HSM toosupport warstwy usługi Premium magazynu kluczy Azure](https://azure.microsoft.com/pricing/free-trial/). Ponadto warto zauważyć, że funkcja ta nie jest dostępna dla chińskiej wersji platformy Azure.

Po utworzeniu magazynu kluczy hello dodać hello **- SKU** parametru:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



Możesz dodać klucze chronione oprogramowaniem (jak pokazano wcześniej) i magazynu kluczy toothis klucze chronione przez moduł HSM. toocreate klucza chronionego przez moduł HSM, ustaw hello **-docelowy** too'HSM parametru ":

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

Można użyć następującego polecenia tooimport hello klucza z. Plik PFX na tym komputerze. To polecenie importuje klucz hello do sprzętowych modułów zabezpieczeń w usłudze Key Vault hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


Witaj następne polecenie importuje "bring your own key" (BYOK) pakietu. Ten scenariusz umożliwia generowanie klucza w lokalnym module HSM i przeniesienie go tooHSMs w hello usługi Key Vault bez opuszczania hello granic modułu HSM klucz hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

Aby uzyskać szczegółowe instrukcje dotyczące toogenerate pakietu BYOK, zobacz [jak toogenerate i przenoszenie kluczy chronionych HSM dla usługi Azure Key Vault](key-vault-hsm-protected-keys.md).

## <a id="delete"></a>Usuń hello magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych
Jeśli nie są już potrzebne hello magazynu kluczy oraz klucz hello lub klucz tajny, który zawiera, można usunąć magazynu kluczy hello za pomocą hello [Remove-AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) polecenia cmdlet:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Lub usunięciem całej grupy zasobów platformy Azure, w tym magazynie kluczy hello i inne zasoby, które zostały dodane do tej grupy:

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>Inne polecenia cmdlet programu Azure PowerShell
Inne polecenia, które mogą być przydatne do zarządzania usługą Azure Key Vault:

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: To polecenie wyświetla tabelaryczny widok wszystkich kluczy i wybranych właściwości.
* `$Keys[0]`: To polecenie wyświetla pełną listę właściwości dla określonego klucza hello
* `Get-AzureKeyVaultSecret`: To polecenie wyświetla tabelaryczny widok wszystkich nazw kluczy tajnych i wybranych właściwości.
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Przykład jak tooremove określonego klucza.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Przykład jak tooremove określonego klucza tajnego.

## <a id="next"></a>Następne kroki
Aby zapoznać się z kolejnym samouczkiem, w którym jest używana usługa Azure Key Vault w aplikacji sieci Web, zobacz artykuł [Użycie usługi Azure Key Vault z aplikacji sieci Web](key-vault-use-from-web-application.md).

toosee Twojego magazynu kluczy jest używany, zobacz [rejestrowanie usługi Azure Key Vault](key-vault-logging.md).

Aby uzyskać listę hello najnowsze Azure poleceń cmdlet programu PowerShell dla usługi Azure Key Vault, zobacz [polecenia cmdlet usługi Azure Key Vault](/powershell/module/azurerm.keyvault/#key_vault).

Odwołania dotyczące programowania, zobacz [hello przewodnik dewelopera usługi Azure Key Vault](key-vault-developers-guide.md).
