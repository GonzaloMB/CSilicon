# Initial findings

**State:** Draft  
**Researched:** 2026-10-07

These findings establish direction; they do not yet prove end-to-end
compatibility.

## Supported platforms are already a product constraint

Valve's current Steam page lists Counter-Strike 2 requirements for Windows and
SteamOS/Linux, but not macOS. The Windows renderer requirement is DirectX 11
with Shader Model 5.0. CSilicon must therefore describe the macOS path as an
unsupported compatibility effort, not a native or officially supported port.

**Evidence:** primary — [Counter-Strike 2 on Steam](https://store.steampowered.com/app/730/CounterStrike_2/)

## DXMT matches the graphics API, with strict prerequisites

DXMT describes itself as a Metal-based Direct3D 11/10 implementation for Wine.
Its upstream specifications require Apple Silicon, macOS Sonoma or later,
Wine 8 or later, and currently focus on 64-bit programs. DXMT also depends on
specific APIs exported by Wine's macOS driver, so arbitrary Wine builds cannot
be assumed compatible.

This supports the core “versioned runtime bundle” design and argues against
discovering a random system Wine at launch time.

**Evidence:** primary — [DXMT device/system/runtime specifications](https://github.com/3Shain/dxmt/wiki/Device-System-Runtime-Specifications), [DXMT development guide](https://github.com/3Shain/dxmt/blob/main/docs/DEVELOPMENT.md)

## Rosetta capabilities help, but the exact execution path needs proof

Apple documents translation of x86_64 instructions, including AVX and AVX2,
on Apple Silicon; AVX-512 is not supported. Apple also documents a platform
transition around macOS 27. This is encouraging for x86_64 game code but does
not by itself prove that a given Wine/DXMT/CS2 composition works. CSilicon must
detect the host OS and translation capability rather than assuming a fixed
Rosetta installation model forever.

**Evidence:** primary — [About the Rosetta translation environment](https://developer.apple.com/documentation/Apple-Silicon/about-the-rosetta-translation-environment)

## VAC compatibility is unresolved

Valve documents anti-cheat and Proton support, but the public material found so
far does not certify CS2/VAC on a third-party macOS Wine/DXMT stack. Therefore:

- offline or explicitly insecure testing comes first;
- “the game launches” does not imply “secure matchmaking is supported”;
- CSilicon must not market itself as VAC-safe without stronger evidence;
- no anti-cheat bypass or game-process inspection belongs in the product.

**Evidence:** primary — [Steamworks anti-cheat documentation](https://partner.steamgames.com/doc/features/anticheat), [Steam Deck and Proton](https://partner.steamgames.com/doc/steamdeck/proton)

FACEIT is a separate, harder boundary. FACEIT states that its anti-cheat is
available for Windows 10/11, not macOS or Linux, and requires Windows security
features including Secure Boot and TPM 2.0. CSilicon can target Valve's normal
VAC matchmaking/Premier, but cannot honestly promise FACEIT support.

**Evidence:** primary — [FACEIT: What is FACEIT anti-cheat?](https://support.faceit.com/hc/es/articles/9394666828188--Qu%C3%A9-es-FACEIT-Anti-cheat-y-c%C3%B3mo-funciona), [FACEIT security requirements](https://support.faceit.com/hc/en-us/articles/12452232454940-Enabling-Security-Requirements)

## Keychain is appropriate later, not required for the base CLI

Apple recommends Keychain Services for small secrets and specifically prefers
the `SecItem` API/data-protection keychain for modern macOS apps. Apple's own
technical note also warns that command-line tools require packaging and
entitlement decisions for that keychain mode. Since the first milestones need
no API key, secrets support should be deferred and designed with the eventual
signed app bundle rather than improvised into `config.toml`.

**Evidence:** primary — [Keychain Services](https://developer.apple.com/documentation/Security/keychain-services), [TN3137: On Mac keychains](https://developer.apple.com/documentation/Technotes/tn3137-on-mac-keychains)

## Preliminary conclusion

The architecture is plausible, but feasibility is not yet demonstrated. The
highest-risk unknowns are the exact Wine/DXMT coupling, Steam bootstrap/update
behavior, CS2 regressions, online/VAC behavior, and redistribution rights.

## Linux does not remove all translation layers

CS2 has a native Linux build, but Valve publishes it for x86_64-class systems;
Valve's Steam for Linux client requirements are also x86_64/AMD64. An Apple
Silicon Mac is ARM64, so the Linux path still needs CPU translation such as FEX,
plus a Linux environment and accelerated Vulkan.

Apple documents x86_64 translation inside ARM Linux VMs, but its documented
Linux graphics device is Virtio GPU 2D. That is not the accelerated Vulkan
gaming path CS2 needs. The Metal-accelerated paravirtualized GPU is documented
for macOS guests, not Linux guests.

Bare-metal Fedora Asahi Remix provides the relevant architecture: Linux on the
hardware, Vulkan drivers, FEX, and `muvm`. However, the current target machine
is an M4 Pro MacBook Pro (`Mac16,8`), for which Asahi currently lists no
installer and no GPU support. Therefore neither Linux VM nor bare-metal Linux
is a viable CSilicon runtime for this machine today.

**Evidence:** primary — [Steam for Linux requirements](https://github.com/ValveSoftware/steam-for-linux/blob/master/README.md), [Apple Linux VM graphics](https://developer.apple.com/videos/play/wwdc2022/10002/), [Asahi gaming architecture](https://asahilinux.org/2024/10/aaa-gaming-on-asahi-linux/), [Asahi M4 support](https://asahilinux.org/docs/platform/feature-support/m4/)

## A current macOS reference implementation exists

CodeWeavers currently rates CS2 as “Runs Well” on CrossOver 26.3 for macOS and
has published Apple Silicon performance tests. This is strong evidence that a
Windows/Wine-based macOS path can launch and play CS2 on suitable hardware. It
does not, by itself, certify every CS2 build or guarantee VAC-secure sessions.

CrossOver should therefore be used as a reference baseline during research,
not silently bundled, copied, or treated as proof that a redistributable
CSilicon Wine/DXMT runtime will behave identically.

**Evidence:** upstream vendor — [CrossOver CS2 compatibility](https://www.codeweavers.com/compatibility/crossover/counter-strike-global-offensive), [CodeWeavers Apple Silicon performance test](https://www.codeweavers.com/blog/mjohnson/2024/03/26/counter-strike-2-x-4-macs-gr8-crossover-content), [CodeWeavers anti-cheat policy](https://support.codeweavers.com/anti-cheat)
