# PixelOS Android 17 — Pixel 4 XL (coral)

Independent snapshot of `Nahida-Prjkt/android_device_google_coral` on
`lineage-24.0`. Exact provenance is recorded in [UPSTREAM.json](UPSTREAM.json).
Existing upstream copyright and license notices remain in place.

The PixelOS product is `custom_coral`, using
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

PixelOS disables the Lineage SDK. The base GoogleParts eSIM boot receiver uses a
local app-label resource instead of `org.lineageos.settings.resources`.
The standalone Motion Sense app supplies its own settings resources.

Use the complete setup, preparation, validation and build instructions in
[Pixelos-localmanifest](https://github.com/its-hecker/Pixelos-localmanifest).
Run preparation again after syncing framework or overlay sources.

Full ROM compilation and PixelOS phone validation are still required. Source
integration checks do not establish runtime success.
