# Changes and Instructions

## 🛠️ Changes Made to MicroG-RE

- **Custom Base Package Name**: Updated `basePackageName` to `"org.microg2"` in [build.gradle](build.gradle) (Application ID: `org.microg2.android.gms`) to bypass Huawei HarmonyOS 6 package blacklists (such as `app.revanced.*`) and avoid conflicts with standard microG installations.
- **Dynamic Package Resolution**: Updated [ForegroundServiceContext.java](play-services-base/core/src/main/java/org/microg/gms/common/ForegroundServiceContext.java) to use `context.getPackageName()` dynamically.
- **App Shortcuts**: Updated target package in [shortcuts.xml](play-services-core/src/main/res/xml-v26/shortcuts.xml) to `org.microg2.android.gms`.
- **Automatic Release Signing**: Configured `signingConfig signingConfigs.debug` for the `release` build type in [play-services-core/build.gradle](play-services-core/build.gradle) so release APKs are automatically signed with certificates.

---

## 🚀 Building & Installation Instructions

### 1. Build the Release APK
From the repository root folder, run:
```powershell
.\gradlew.bat :play-services-core:assembleRelease
```

- **Output File**: `play-services-core\build\outputs\apk\huawei\release\microg-release-6.1.4.apk`



---

## 🧩 Morphe Patching Instructions (HarmonyOS 6 / Custom Package)

When patching YouTube / target app to work with `org.microg2.android.gms`:

1. **Custom Patches Repository**: Use the custom [https://github.com/AndrewKeYanzhe/morphe-patches](https://github.com/AndrewKeYanzhe/morphe-patches) repo configured with `GMS_CORE_VENDOR_GROUP_ID = "org.microg2"`.
2. **Package Visibility & Popups**: Adds `QUERY_ALL_PACKAGES` permission in `AndroidManifest.xml` and neutralizes `checkGmsCore` popups to prevent browser redirect loops.
3. **Fast Patching on PC**: Use the GUI **Morphe Desktop** app (`morphe-desktop.jar`) to patch your target APK. Load both **`patches-1.37.0.mpp`** and its matching **`patches-1.37.0.json`** metadata file into Morphe Desktop along with your target APK to patch.
4. **HarmonyOS 6 MicroG Settings Access**:
   - On the phone, navigate to: `卓易通` ➔ `我的` ➔ `应用管理` ➔ `MicroG RE` ➔ `⚙️ Settings / Gear icon`.
   - Access MicroG RE settings to manage permissions and disable battery optimizations.

---

<div align="center"> 
<picture>
    <source
      width="512px"
      media="(prefers-color-scheme: dark)"
      srcset="https://raw.githubusercontent.com/MorpheApp/.github/refs/heads/main/profile/assets/morphe-wordmark/morphe_wordmark_dark.svg"
    />
    <img 
      width="512px"
      src="https://raw.githubusercontent.com/MorpheApp/.github/refs/heads/main/profile/assets/morphe-wordmark/morphe_wordmark_light.svg"
    />
</picture>

[![Website badge](https://img.shields.io/badge/Website-gray.svg?logo=data:image/svg%2bxml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+CjwhLS0gQ29weXJpZ2h0IDIwMjUgTW9ycGhlLiBUaGlzIGlzIGNvcHlyaWdodGVkIGNvbnRlbnQsIGFuZCBub3QgbGljZW5zZWQgdW5kZXIgb3BlbiBzb3VyY2UgdGVybXMuCiAgICAgU2VlIGh0dHBzOi8vZ2l0aHViLmNvbS9Nb3JwaGVBcHAvbW9ycGhlLWJyYW5kaW5nIC0tPgoKPHN2ZwogICB3aWR0aD0iNTEyIgogICBoZWlnaHQ9IjUxMiIKICAgdmlld0JveD0iMCAwIDUxMiA1MTIiCiAgIHZlcnNpb249IjEuMSIKICAgaWQ9InN2ZzIiCiAgIHNvZGlwb2RpOmRvY25hbWU9Im1vcnBoZV9sb2dvX2xpZ2h0LnN2ZyIKICAgaW5rc2NhcGU6dmVyc2lvbj0iMS40LjIgKGViZjBlOTQwZDAsIDIwMjUtMDUtMDgpIgogICB4bWxuczppbmtzY2FwZT0iaHR0cDovL3d3dy5pbmtzY2FwZS5vcmcvbmFtZXNwYWNlcy9pbmtzY2FwZSIKICAgeG1sbnM6c29kaXBvZGk9Imh0dHA6Ly9zb2RpcG9kaS5zb3VyY2Vmb3JnZS5uZXQvRFREL3NvZGlwb2RpLTAuZHRkIgogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciCiAgIHhtbG5zOnN2Zz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogIDxzb2RpcG9kaTpuYW1lZHZpZXcKICAgICBpZD0ibmFtZWR2aWV3MiIKICAgICBwYWdlY29sb3I9IiNmZmZmZmYiCiAgICAgYm9yZGVyY29sb3I9IiMwMDAwMDAiCiAgICAgYm9yZGVyb3BhY2l0eT0iMC4yNSIKICAgICBpbmtzY2FwZTpzaG93cGFnZXNoYWRvdz0iMiIKICAgICBpbmtzY2FwZTpwYWdlb3BhY2l0eT0iMC4wIgogICAgIGlua3NjYXBlOnBhZ2VjaGVja2VyYm9hcmQ9IjAiCiAgICAgaW5rc2NhcGU6ZGVza2NvbG9yPSIjZDFkMWQxIgogICAgIGlua3NjYXBlOnpvb209IjEuMTU0Mjk2OSIKICAgICBpbmtzY2FwZTpjeD0iMjU2IgogICAgIGlua3NjYXBlOmN5PSIyNTYiCiAgICAgaW5rc2NhcGU6d2luZG93LXdpZHRoPSIxNDQwIgogICAgIGlua3NjYXBlOndpbmRvdy1oZWlnaHQ9IjgzNiIKICAgICBpbmtzY2FwZTp3aW5kb3cteD0iMCIKICAgICBpbmtzY2FwZTp3aW5kb3cteT0iMCIKICAgICBpbmtzY2FwZTp3aW5kb3ctbWF4aW1pemVkPSIxIgogICAgIGlua3NjYXBlOmN1cnJlbnQtbGF5ZXI9InN2ZzIiPgogICAgPGlua3NjYXBlOnBhZ2UKICAgICAgIHg9IjAiCiAgICAgICB5PSIwIgogICAgICAgd2lkdGg9IjUxMiIKICAgICAgIGhlaWdodD0iNTEyIgogICAgICAgaWQ9InBhZ2UyIgogICAgICAgbWFyZ2luPSIwIgogICAgICAgYmxlZWQ9IjAiIC8+CiAgPC9zb2RpcG9kaTpuYW1lZHZpZXc+CiAgPGRlZnMKICAgICBpZD0iZGVmczIiIC8+CiAgPCEtLSBMZXR0ZXIgLS0+CiAgPGcKICAgICBpZD0iTGV0dGVyIgogICAgIHN0eWxlPSJmaWxsOiNmZmZmZmY7ZmlsbC1vcGFjaXR5OjEiPgogICAgPHBhdGgKICAgICAgIGlkPSJMZWZ0IgogICAgICAgZD0ibSAxMjMsMTQwIGMgLTIxLDAgLTM5LDE3IC00MCwzOCB2IDE5MiBjIDEsMjEgMTksMzggNDAsMzggMjEsMCAzOSwtMTcgNDAsLTM4IFYgMTc4IGMgLTEsLTIxIC0xOSwtMzggLTQwLC0zOCB6IgogICAgICAgZmlsbD0iIzFFNUFBOCIKICAgICAgIHN0eWxlPSJmaWxsOiNmZmZmZmY7ZmlsbC1vcGFjaXR5OjEiIC8+CiAgICA8cGF0aAogICAgICAgaWQ9IlJpZ2h0IgogICAgICAgZD0ibSAzNDksMjg1IHYgODUgYyAxLDIxIDE5LDM4IDQwLDM4IDIxLDAgMzksLTE3IDQwLC0zOCBWIDE4MiBjIC0xMSwtMTQgLTc0LDYzIC04MCwxMDMgeiIKICAgICAgIGZpbGw9IiMwMEFGQUUiCiAgICAgICBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxIiAvPgogICAgPHBhdGgKICAgICAgIGlkPSJNaWRkbGUiCiAgICAgICBkPSJtIDEyNywxMDggYyAtMzQsMCAtNDQsMjUgLTQ0LDQwIHYgNTQgYyAzMCwtMzMgNzUsMjcgODAsMzMgMjgsMzIgNDQsODcgOTMsODkgNDgsLTIgNjcsLTU2IDkzLC04OSAwLDAgNDUsLTc0IDgwLC04MCAwLC0yOCAtMTEsLTQ3IC00NCwtNDcgLTM0LDAgLTU4LDUwIC03NSw3MiAtMTcsMjIgLTI1LDQ2IC01NCw0NiAtMjksMCAtMzgsLTI1IC01NCwtNDYgLTE3LC0yMiAtNDEsLTcyIC03NSwtNzIgeiIKICAgICAgIGZpbGw9InVybCgjbGluZWFyR3JhZGllbnQyKSIKICAgICAgIHN0eWxlPSJmaWxsOiNmZmZmZmY7ZmlsbC1vcGFjaXR5OjEiIC8+CiAgPC9nPgo8L3N2Zz4K&style=for-the-badge)](https://morphe.software) [![Subreddit badge](https://img.shields.io/badge/Reddit-gray?style=for-the-badge&logo=reddit&logoColor=white)](https://www.reddit.com/r/MorpheApp) [![X badge](https://img.shields.io/badge/X_-gray?style=for-the-badge&logo=x)](https://x.com/MorpheApp) [![Crowdin badge](https://img.shields.io/badge/Translations-gray?style=for-the-badge&logo=crowdin)](https://morphe.software/translate)
<br>
</div> 

&nbsp;
<p align="center">
  <a href="https://morphe.software" title="Download Morphe">
    <img src="https://raw.githubusercontent.com/MorpheApp/.github/refs/heads/main/profile/assets/download-morphe.svg" alt="Download Morphe" width="240"/>
  </a>
</p>
&nbsp;

# ⚙️ MicroG RE (GmsCore Redesign)

[GmsCore](https://github.com/microg/GmsCore) fork for Morphe patched apps with [Material 3 Expressive](https://m3.material.io/blog/building-with-m3-expressive) design, enhanced features, and improvements.

This repository is a fork of [microG GmsCore](https://github.com/microg/GmsCore), adapted to work with patched Google apps without requiring root access and under an alternative package name. It uses the **GmsCore support** patch from Morphe Patches to enable Google account authentication and services, replacing Google Play Services.

## 🤝 Credits

- [microG Project](https://github.com/microg) for GmsCore, alternative of Play Services. [wiki](https://github.com/microg/GmsCore/wiki)

- [Shadow578](https://github.com/shadow578) and [ReVanced Team](https://github.com/ReVanced) for the implementation of ReVanced GmsCore group ID vendor.

- [AyushTNM](https://github.com/ayushTNM) for some useful implementations and ideas.

- All legacy Vanced Team for the inspiration of some of the features.

[See all contributors](https://github.com/MorpheApp/MicroG-RE/graphs/contributors)

## 📜 License

    Copyright 2013-2025 microG Project Team

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
