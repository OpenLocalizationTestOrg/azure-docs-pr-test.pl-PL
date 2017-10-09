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
## <a name="setting-up-your-ios-application"></a>Konfigurowanie aplikacji systemu iOS

Ta sekcja zawiera instrukcje krok po kroku toocreate nowe toodemonstrate projektu jak toointegrate aplikacji systemu iOS (Swift) z *logowania z firmą Microsoft* aby mogła zbadać interfejsów API sieci Web, które wymagają tokenu.

> Preferowane projektu XCode ten przykład toodownload zamiast niego? [Pobieranie projektu](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) i pominąć toohello [kroku konfiguracji](#create-an-application-express) przykładowy kod hello tooconfigure przed wykonaniem.


## <a name="install-carthage-toodownload-and-build-msal"></a>Zainstaluj Carthage toodownload i kompilacji MSAL
Carthage Menedżera pakietów jest używana w okresie Podgląd hello MSAL — integruje się z XCode przy zachowaniu możliwości hello Microsoft toomake zmiany toohello biblioteki.

- Pobierz i zainstaluj najnowszą wersję hello Carthage [tutaj](https://github.com/Carthage/Carthage/releases "Carthage adresu URL pobierania")

## <a name="creating-your-application"></a>Tworzenie aplikacji

1.  Otwórz środowisko Xcode i wybierz pozycję`Create a new Xcode project`
2.  Wybierz `iOS`  >  `Single view Application` i kliknij przycisk *dalej*
3.  Nadaj nazwę produktu, a następnie kliknij przycisk *dalej*
4.  Wybierz folder toocreate aplikacji i kliknij *Utwórz*

## <a name="build-hello-msal-framework"></a>Tworzenie hello MSAL Framework

Postępuj zgodnie z instrukcjami hello poniżej toopull i późniejszego kompilowania hello najnowszej wersji biblioteki MSAL przy użyciu Carthage:

1.  Otwórz hello bash terminal i przejdź do folderu głównego toohello aplikacji
2.  Poniżej hello kopiowania i wklejania w hello bash terminali toocreate pliku "Cartfile":

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Skopiuj i Wklej hello poniżej. To polecenie pobiera zależności do folderu Carthage/wyewidencjonowania, a następnie tworzy hello MSAL biblioteki:
</li>
</ol>

```bash
carthage update
```

> proces Hello powyżej jest używane toodownload i kompilacji hello biblioteki uwierzytelniania firmy Microsoft (MSAL). MSAL obsługuje pobieranie, buforowanie i odświeżanie użytkownika tokenów używanych tooaccess interfejsów API chronione przez hello Azure Active Directory w wersji 2.

## <a name="add-hello-msal-framework-tooyour-application"></a>Dodawanie hello MSAL framework tooyour aplikacji
1.  W środowisku Xcode Otwórz hello `General` kartę
2.  Przejdź toohello `Linked Frameworks and Libraries` sekcji, a następnie kliknij przycisk`+`
3.  Wybierz pozycję `Add other…`
4.  Wybierz: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` i kliknij przycisk *Otwórz*. Powinny pojawić się `MSAL.framework` dodane toohello listy.
5.  Przejdź za`Build Phases` , a następnie kliknij pozycję `+` ikony, wybierz pozycję`New Run Script Phase`
6.  Dodaj powitania po toohello zawartość *skryptu obszaru*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Dodaje hello zbyt<code>Input Files</code> klikając <code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>Tworzenie aplikacji interfejsu użytkownika
Plik Main.storyboard należy utworzyć automatycznie w ramach szablonu projektu. Wykonaj instrukcje hello poniżej aplikacji hello toocreate interfejsu użytkownika:

1.  Kontrolowanie i kliknięcia `Main.storyboard` toobring menu kontekstowe hello w górę, a następnie kliknij pozycję:`Open As` > `Source Code`
2.  Zastąp hello `<scenes>` węzła z kodem hello poniżej:

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
