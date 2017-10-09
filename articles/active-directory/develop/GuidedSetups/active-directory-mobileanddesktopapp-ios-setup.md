---
title: iOS v2 aaaAzure AD Getting Started - Instalator | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="769f3-103">Konfigurowanie aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="769f3-103">Setting up your iOS application</span></span>

<span data-ttu-id="769f3-104">Ta sekcja zawiera instrukcje krok po kroku toocreate nowe toodemonstrate projektu jak toointegrate aplikacji systemu iOS (Swift) z *logowania z firmą Microsoft* aby mogła zbadać interfejsów API sieci Web, które wymagają tokenu.</span><span class="sxs-lookup"><span data-stu-id="769f3-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="769f3-105">Preferowane projektu XCode ten przykład toodownload zamiast niego?</span><span class="sxs-lookup"><span data-stu-id="769f3-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="769f3-106">[Pobieranie projektu](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) i pominąć toohello [kroku konfiguracji](#create-an-application-express) przykładowy kod hello tooconfigure przed wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="769f3-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="769f3-107">Zainstaluj Carthage toodownload i kompilacji MSAL</span><span class="sxs-lookup"><span data-stu-id="769f3-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="769f3-108">Carthage Menedżera pakietów jest używana w okresie Podgląd hello MSAL — integruje się z XCode przy zachowaniu możliwości hello Microsoft toomake zmiany toohello biblioteki.</span><span class="sxs-lookup"><span data-stu-id="769f3-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="769f3-109">Pobierz i zainstaluj najnowszą wersję hello Carthage [tutaj](https://github.com/Carthage/Carthage/releases "Carthage adresu URL pobierania")</span><span class="sxs-lookup"><span data-stu-id="769f3-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="769f3-110">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="769f3-110">Creating your application</span></span>

1.  <span data-ttu-id="769f3-111">Otwórz środowisko Xcode i wybierz pozycję`Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="769f3-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="769f3-112">Wybierz `iOS`  >  `Single view Application` i kliknij przycisk *dalej*</span><span class="sxs-lookup"><span data-stu-id="769f3-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="769f3-113">Nadaj nazwę produktu, a następnie kliknij przycisk *dalej*</span><span class="sxs-lookup"><span data-stu-id="769f3-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="769f3-114">Wybierz folder toocreate aplikacji i kliknij *Utwórz*</span><span class="sxs-lookup"><span data-stu-id="769f3-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="769f3-115">Tworzenie hello MSAL Framework</span><span class="sxs-lookup"><span data-stu-id="769f3-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="769f3-116">Postępuj zgodnie z instrukcjami hello poniżej toopull i późniejszego kompilowania hello najnowszej wersji biblioteki MSAL przy użyciu Carthage:</span><span class="sxs-lookup"><span data-stu-id="769f3-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="769f3-117">Otwórz hello bash terminal i przejdź do folderu głównego toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="769f3-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="769f3-118">Poniżej hello kopiowania i wklejania w hello bash terminali toocreate pliku "Cartfile":</span><span class="sxs-lookup"><span data-stu-id="769f3-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="769f3-119">Skopiuj i Wklej hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="769f3-119">Copy and paste hello below.</span></span> <span data-ttu-id="769f3-120">To polecenie pobiera zależności do folderu Carthage/wyewidencjonowania, a następnie tworzy hello MSAL biblioteki:</span><span class="sxs-lookup"><span data-stu-id="769f3-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="769f3-121">proces Hello powyżej jest używane toodownload i kompilacji hello biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="769f3-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="769f3-122">MSAL obsługuje pobieranie, buforowanie i odświeżanie użytkownika tokenów używanych tooaccess interfejsów API chronione przez hello Azure Active Directory w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="769f3-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="769f3-123">Dodawanie hello MSAL framework tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="769f3-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="769f3-124">W środowisku Xcode Otwórz hello `General` kartę</span><span class="sxs-lookup"><span data-stu-id="769f3-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="769f3-125">Przejdź toohello `Linked Frameworks and Libraries` sekcji, a następnie kliknij przycisk`+`</span><span class="sxs-lookup"><span data-stu-id="769f3-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="769f3-126">Wybierz pozycję `Add other…`</span><span class="sxs-lookup"><span data-stu-id="769f3-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="769f3-127">Wybierz: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` i kliknij przycisk *Otwórz*.</span><span class="sxs-lookup"><span data-stu-id="769f3-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="769f3-128">Powinny pojawić się `MSAL.framework` dodane toohello listy.</span><span class="sxs-lookup"><span data-stu-id="769f3-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="769f3-129">Przejdź za`Build Phases` , a następnie kliknij pozycję `+` ikony, wybierz pozycję`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="769f3-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="769f3-130">Dodaj powitania po toohello zawartość *skryptu obszaru*:</span><span class="sxs-lookup"><span data-stu-id="769f3-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="769f3-131">Dodaje hello zbyt<code>Input Files</code> klikając <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="769f3-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="769f3-132">Tworzenie aplikacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="769f3-132">Creating your application’s UI</span></span>
<span data-ttu-id="769f3-133">Plik Main.storyboard należy utworzyć automatycznie w ramach szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="769f3-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="769f3-134">Wykonaj instrukcje hello poniżej aplikacji hello toocreate interfejsu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="769f3-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="769f3-135">Kontrolowanie i kliknięcia `Main.storyboard` toobring menu kontekstowe hello w górę, a następnie kliknij pozycję:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="769f3-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="769f3-136">Zastąp hello `<scenes>` węzła z kodem hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="769f3-136">Replace hello `<scenes>` node with hello code below:</span></span>

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
