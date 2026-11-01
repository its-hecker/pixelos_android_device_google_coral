# PixelOS Android 17 — Pixel 4 / Pixel 4 XL

Independent snapshot of `Nahida-Prjkt/android_device_google_coral` on
`lineage-24.0`. Exact provenance is recorded in [UPSTREAM.json](UPSTREAM.json).
Existing upstream copyright and license notices remain in place.

The PixelOS products are `custom_coral` (Pixel 4 XL) and `custom_flame` (Pixel 4), using
`vendor/custom/config/common_full_phone.mk`. PixelOS's software ParanoidSense
provider is disabled before common inheritance. The real hardware Face provider
and Motion Sense UI/compatibility are inherited **after** the base vendor product
from these standalone repositories:

- [Floral Motion Sense](https://github.com/its-hecker/floral-motionsense-plugin)
- [Floral 3D Face ID](https://github.com/its-hecker/floral-3D-faceid-plugin)

The plugins own their generated overlays, native compatibility libraries,
framework fixes and additional SELinux policy. No integrated Infinity Motion
Sense pages, camera shim source or wallpaper modifications were copied here.
The unused stock Oslo application domain and debug labels are removed so the
plugin owns one consistent platform policy and its generated property labels.
The stock CHRE/Soli, IR camera, Airbrush, Citadel, firmware and calibration
requirements remain supplied by the device/vendor/kernel base.

General fixes retained from the working Infinity tree:

- HardwareInfo is a platform `coredomain`; obsolete direct battery sysfs grants
  are removed.
- `ro.hwui.render_ahead` is defined by system properties instead of vendor init.
- Mainline modules are built from source, with APEX contributions ignored.
- Lunaris Dolby inheritance is optional; the local manifest supplies it.
- The camera's 64-bit legacy thermal interface is explicitly packaged.

The stock camera service uses the build module
`android.hardware.camera.provider@2.7-service-google-coral`, with the original
executable name supplied through `stem`. Its extraction entry keeps this suffix
when vendor makefiles are regenerated. This prevents Soong from joining the
stock AIDL V1 dependencies to the newer AOSP source service's dependencies.
The installed binary, init service and VINTF interface remain the stock ones.

PixelOS disables the Lineage SDK. The base GoogleParts eSIM boot receiver uses a
local app-label resource instead of `org.lineageos.settings.resources`.
The standalone Motion Sense app supplies its own settings resources.

Artifact-path validation remains enabled in `relaxed` mode. The product allows
the eight exact system paths used by PixelOS's Google ExtServices, ExtShared,
print recommendation, TensorFlow Lite, DocumentsUI, NFC Tag and privileged
permission configuration.
Other additions to the generic system product remain subject to validation.

Use the complete setup, preparation, validation and build instructions in
[Pixelos-localmanifest](https://github.com/its-hecker/Pixelos-localmanifest).
For Pixel 4, use
[pixelos-flame-local-manifest](https://github.com/its-hecker/pixelos-flame-local-manifest).
Both manifests check out this shared tree at `device/google/coral`; Flame uses
its own `flame/device.mk`, display configuration, `flame/BoardConfig.mk`,
`vendor/google/flame` and stock Flame build fingerprint. The camera module's
`-coral` suffix and `GoogleCameraCoral` app name are shared build identifiers.
They do not select Coral's vendor images or change Flame's device identity.
Run preparation again after syncing framework or overlay sources.

Full ROM compilation and PixelOS phone validation are still required. Source
integration checks do not establish runtime success.

Flame development lives on the separate `pixelos-flame` branch. The stable
Coral `main` branch is left unchanged. The Flame manifest selects this branch
and pins its exact commit; Coral keeps its existing manifest and stable pins.
