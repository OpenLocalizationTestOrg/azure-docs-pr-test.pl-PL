---
title: Azure AD w wersji 2 dla systemu iOS Getting Started - Instalator | Dokumentacja firmy Microsoft
description: "Jak aplikacje systemu iOS (Swift) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: d25353a61b2a60bff28aa0679d38110e77d19e64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="d4613-103">Konfigurowanie aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="d4613-103">Setting up your iOS application</span></span>

<span data-ttu-id="d4613-104">Ta sekcja zawiera instrukcje krok po kroku dotyczące sposobu tworzenia nowego projektu aby zademonstrować sposób integracji aplikacji systemu iOS (Swift) z *logowania z firmą Microsoft* aby mogła zbadać interfejsów API sieci Web, które wymagają tokenu.</span><span class="sxs-lookup"><span data-stu-id="d4613-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="d4613-105">Preferowane jest zamiast tego Pobierz ten przykład XCode projekt?</span><span class="sxs-lookup"><span data-stu-id="d4613-105">Prefer to download this sample's XCode project instead?</span></span> <span data-ttu-id="d4613-106">[Pobieranie projektu](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) i przejść [kroku konfiguracji](#create-an-application-express) skonfigurować przykładowy kod przed wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="d4613-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


## <a name="install-carthage-to-download-and-build-msal"></a><span data-ttu-id="d4613-107">Zainstaluj Carthage do pobrania i kompilacji MSAL</span><span class="sxs-lookup"><span data-stu-id="d4613-107">Install Carthage to download and build MSAL</span></span>
<span data-ttu-id="d4613-108">Menedżer pakietów Carthage jest używana w okresie Podgląd MSAL — integruje się z XCode przy zachowaniu możliwości dla firmy Microsoft wprowadzić zmiany w bibliotece.</span><span class="sxs-lookup"><span data-stu-id="d4613-108">Carthage package manager is used during the preview period of MSAL – it integrates with XCode while maintaining the ability for Microsoft to make changes to the library.</span></span>

- <span data-ttu-id="d4613-109">Pobierz i zainstaluj najnowszą wersję Carthage [tutaj](https://github.com/Carthage/Carthage/releases "Carthage adresu URL pobierania")</span><span class="sxs-lookup"><span data-stu-id="d4613-109">Download and install the latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="d4613-110">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="d4613-110">Creating your application</span></span>

1.  <span data-ttu-id="d4613-111">Otwórz środowisko Xcode i wybierz pozycję`Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="d4613-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="d4613-112">Wybierz `iOS`  >  `Single view Application` i kliknij przycisk *dalej*</span><span class="sxs-lookup"><span data-stu-id="d4613-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="d4613-113">Nadaj nazwę produktu, a następnie kliknij przycisk *dalej*</span><span class="sxs-lookup"><span data-stu-id="d4613-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="d4613-114">Wybierz folder do utworzenia aplikacji, a następnie kliknij przycisk *Utwórz*</span><span class="sxs-lookup"><span data-stu-id="d4613-114">Select a folder to create your app and click *Create*</span></span>

## <a name="build-the-msal-framework"></a><span data-ttu-id="d4613-115">Tworzenie MSAL Framework</span><span class="sxs-lookup"><span data-stu-id="d4613-115">Build the MSAL Framework</span></span>

<span data-ttu-id="d4613-116">Postępuj zgodnie z instrukcjami poniżej, aby pobierać i późniejszego kompilowania najnowszej wersji biblioteki MSAL przy użyciu Carthage:</span><span class="sxs-lookup"><span data-stu-id="d4613-116">Follow the instructions below to pull and then build the latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="d4613-117">Otwórz bash terminal i przejdź do folderu głównego aplikacji</span><span class="sxs-lookup"><span data-stu-id="d4613-117">Open the bash terminal and go to the App’s root folder</span></span>
2.  <span data-ttu-id="d4613-118">Kopiuj poniżej i Wklej w terminalu bash, aby utworzyć plik "Cartfile":</span><span class="sxs-lookup"><span data-stu-id="d4613-118">Copy the below and paste in the bash terminal to create a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="d4613-119">Skopiuj i Wklej poniżej.</span><span class="sxs-lookup"><span data-stu-id="d4613-119">Copy and paste the below.</span></span> <span data-ttu-id="d4613-120">To polecenie pobiera zależności do folderu Carthage/wyewidencjonowania, a następnie tworzy bibliotekę MSAL:</span><span class="sxs-lookup"><span data-stu-id="d4613-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds the MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="d4613-121">Proces powyżej służy do pobierania i tworzenie biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="d4613-121">The process above is used to download and build the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="d4613-122">MSAL obsługuje pobieranie, buforowanie i odświeżanie tokenów użytkownika, które umożliwiają dostęp do interfejsów API chronione przez usługi Azure Active Directory w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="d4613-122">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by the Azure Active Directory v2.</span></span>

## <a name="add-the-msal-framework-to-your-application"></a><span data-ttu-id="d4613-123">Dodaj platformę MSAL do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d4613-123">Add the MSAL framework to your application</span></span>
1.  <span data-ttu-id="d4613-124">W środowisku Xcode Otwórz `General` kartę</span><span class="sxs-lookup"><span data-stu-id="d4613-124">In Xcode, open the `General` tab</span></span>
2.  <span data-ttu-id="d4613-125">Przejdź do `Linked Frameworks and Libraries` sekcji, a następnie kliknij przycisk`+`</span><span class="sxs-lookup"><span data-stu-id="d4613-125">Go to the `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="d4613-126">Wybierz pozycję `Add other…`</span><span class="sxs-lookup"><span data-stu-id="d4613-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="d4613-127">Wybierz: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` i kliknij przycisk *Otwórz*.</span><span class="sxs-lookup"><span data-stu-id="d4613-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="d4613-128">Powinny pojawić się `MSAL.framework` dodany do listy.</span><span class="sxs-lookup"><span data-stu-id="d4613-128">You should see `MSAL.framework` added to the list.</span></span>
5.  <span data-ttu-id="d4613-129">Przejdź do `Build Phases` , a następnie kliknij pozycję `+` ikony, wybierz pozycję`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="d4613-129">Go to `Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="d4613-130">Dodaj następującą zawartość do *skryptu obszaru*:</span><span class="sxs-lookup"><span data-stu-id="d4613-130">Add the following contents to the *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="d4613-131">Dodaj następujący kod do <code>Input Files</code> klikając <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="d4613-131">Add the following to <code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="d4613-132">Tworzenie aplikacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d4613-132">Creating your application’s UI</span></span>
<span data-ttu-id="d4613-133">Plik Main.storyboard należy utworzyć automatycznie w ramach szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="d4613-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="d4613-134">Postępuj zgodnie z instrukcjami poniżej, aby utworzyć aplikację interfejsu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="d4613-134">Follow the instructions below to create the app UI:</span></span>

1.  <span data-ttu-id="d4613-135">Kontrolowanie i kliknięcia `Main.storyboard` wyświetlić menu kontekstowe, a następnie kliknij przycisk:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="d4613-135">Control+click `Main.storyboard` to bring up the contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="d4613-136">Zastąp `<scenes>` węzła przy użyciu poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="d4613-136">Replace the `<scenes>` node with the code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
