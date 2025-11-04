# iOS 엔터프라이즈 앱 배포 문제 해결 가이드

## 현재 설정 확인사항

### ✅ 확인된 사항
1. **manifest.plist**: bundle-identifier 포함됨 (필수)
2. **IPA 파일**: 정상적으로 업로드됨 (235KB)
3. **아이콘 파일**: icon-57.png, icon-512.png 존재
4. **HTTPS**: GitHub Pages가 자동으로 HTTPS 제공
5. **파일 경로**: 모든 URL이 올바르게 설정됨

### 📋 체크리스트

#### 1. manifest.plist 확인
- ✅ bundle-identifier: com.truefriend.actguid
- ✅ bundle-version: 1.0.0
- ✅ IPA URL: https://ohkst.github.io/actguideinc/poeact.ipa
- ✅ 아이콘 URL: icon-57.png, icon-512.png

#### 2. IPA 파일 확인
- ✅ 파일 존재: poeact.ipa
- ✅ 파일 크기: 235KB
- ✅ 파일 구조: Payload/LifeTracker.app 포함

#### 3. 설치 링크 확인
```
itms-services://?action=download-manifest&url=https://ohkst.github.io/actguideinc/manifest.plist
```

## 가능한 문제 원인

### 1. Enterprise 인증서 문제
- Enterprise 인증서가 IPA 파일에 포함되어 있는지 확인
- embedded.mobileprovision 파일이 올바른지 확인

### 2. iOS 기기 설정
- 설정 > 일반 > VPN 및 기기 관리에서 개발자 신뢰
- "신뢰할 수 없는 개발자" 오류 해결

### 3. 네트워크 문제
- Safari에서 직접 manifest.plist URL 접근 테스트
- IPA 파일 다운로드 테스트

### 4. iOS 버전 문제
- iOS 17.0+ 필요
- Enterprise 배포는 iOS 9.0+ 지원

## 테스트 방법

1. **Safari에서 직접 테스트**
   ```
   https://ohkst.github.io/actguideinc/manifest.plist
   ```
   - 파일이 정상적으로 표시되는지 확인

2. **IPA 파일 직접 다운로드 테스트**
   ```
   https://ohkst.github.io/actguideinc/poeact.ipa
   ```
   - 파일이 다운로드되는지 확인

3. **설치 링크 테스트**
   - iOS 기기의 Safari에서 웹페이지 접속
   - "앱 설치하기" 버튼 탭
   - 설치 프로세스 확인

## 디버깅 정보

### IPA 파일 구조
```
Payload/
  LifeTracker.app/
    _CodeSignature/
    embedded.mobileprovision
    Info.plist
    act guide.md
    LifeTracker (실행 파일)
    Assets.car
```

### manifest.plist 구조
```xml
- items
  - assets
    - software-package: poeact.ipa
    - display-image: icon-57.png
    - full-size-image: icon-512.png
  - metadata
    - bundle-identifier: com.truefriend.actguid
    - bundle-version: 1.0.0
    - title: POEAct
```

## 추가 확인사항

1. **Provisioning Profile 확인**
   - Enterprise 배포용 인증서인지 확인
   - 인증서가 만료되지 않았는지 확인

2. **Bundle ID 확인**
   - IPA 파일 내부의 Bundle ID가 manifest.plist와 일치하는지 확인
   - Info.plist의 CFBundleIdentifier 확인

3. **GitHub Pages 설정**
   - Pages가 활성화되어 있는지 확인
   - 배포 브랜치가 "main"인지 확인

