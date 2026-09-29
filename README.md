# Reclaim Android v1.0.3 — Hard Lock

This source build adds the requested Locked Mode hardening:

- Website Blocker and LAN Sync foreground-service channels moved to hidden/minimum-visibility channels.
- Locked sessions cannot be stopped through the normal UI or by changing focus/website settings.
- Settings, package installer/uninstaller, permission controller and Play Store escape routes are blocked by the accessibility service while Locked Mode is active.
- Device Admin must be enabled before a Locked session starts. If the app is provisioned as Device Owner, uninstall blocking is applied automatically for the session.
- Locked Mode survives reboot and re-engages its policy on boot.
- Emergency unlock is the only in-app early exit: configurable cooldown plus at least 1,200 manually typed characters; large pasted blocks are rejected and the event is logged.
- Windows pairing/enforcement settings are frozen during Locked Mode.

## Device Owner (optional strongest uninstall protection)
Android does not allow a normal app to silently make itself Device Owner. On a dedicated/fresh test device, Device Owner provisioning can be performed with ADB before normal device setup, then Reclaim can enforce `setUninstallBlocked()` during Locked Mode. Device Admin still adds uninstall friction on normal personal devices.


## v1.0.5 Locked Mode start fix
- Locked one-tap and quick sessions now use Android's Device Admin result flow.
- The session starts automatically only after Device Admin is confirmed active.
- Settings is temporarily exempted only while the Device Admin activation screen is open, preventing the blocker from bouncing the activation screen away.
- Denying/cancelling Device Admin leaves the session stopped.
