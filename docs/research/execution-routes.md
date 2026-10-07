# Execution route comparison

**State:** Proposed  
**Decision date:** 2026-10-07

The goal is full CS2 use, including Valve matchmaking/Premier, from the target
Apple Silicon Macs. “Launches the menu” is insufficient. FACEIT is excluded:
its vendor currently supplies the required anti-cheat only for Windows 10/11,
not macOS or Linux, and requires Windows platform-security features.

## Route comparison

| Route | CPU/ABI path | Graphics path | Online status | Product fit |
|---|---|---|---|---|
| macOS + Windows CS2 | x86_64 Windows through Wine and Apple translation/FEX | D3D11 to DXMT/D3DMetal to Metal | VAC requires validation | selected candidate |
| Linux VM on macOS | x86_64 Linux through translation in ARM Linux guest | documented Virtio GPU 2D | untested | reject for gaming |
| Bare-metal Asahi + Linux CS2 | x86_64 Linux through FEX/muvm | Vulkan through Asahi GPU driver | VAC requires validation | not a macOS-wide solution |
| Remote Windows PC/cloud | native supported Windows host, streamed to Mac | remote GPU | provider/host dependent | outside local-first scope |

## Why the Linux build is not directly runnable on macOS

“Linux” identifies an operating-system ABI, not only a file format. The CS2
Linux executable expects Linux system calls and x86_64 userspace libraries.
macOS on Apple Silicon provides neither directly. It needs:

1. an ARM Linux kernel/environment;
2. x86_64-to-ARM translation for Steam and CS2;
3. the Steam Linux runtime and supporting libraries;
4. Vulkan acceleration exposed to the game;
5. working input, audio, networking, and Steam/VAC integration.

## Linux VM decision

Apple supports translating x86_64 applications inside an ARM Linux VM. However,
Apple describes Linux graphics through Virtio GPU 2D: Linux renders a surface
and supplies it to macOS for display. Apple's Metal-accelerated
ParavirtualizedGraphics stack is documented for macOS guests. Without a
supported accelerated Vulkan path, this route cannot satisfy CS2 performance.

**Decision:** do not build CSilicon around a Linux VM. Revisit only if Apple or
a production-grade supported virtualization stack exposes the required Vulkan
feature set and performance.

## Bare-metal Asahi decision

Asahi's gaming stack is technically relevant: its Vulkan driver plus FEX and
`muvm` can run x86/x86_64 applications on ARM Linux. It also avoids translating
D3D11 when using CS2's Linux/Vulkan build.

Asahi support varies substantially by Apple Silicon generation and device.
Even on supported systems, this route requires disk partitioning and rebooting
out of macOS. It cannot satisfy a product promise that should work from macOS
across multiple supported Mac families.

**Decision:** keep Asahi as a monitored alternative, not an implementation
target for CSilicon's macOS runtime.

## Selected research route

Use the Windows build on macOS. First establish an external reference with the
current CrossOver CS2 recipe. Then determine whether CSilicon can reproduce the
required behavior with a legally redistributable, pinned Wine/DXMT runtime.

Online validation is a separate gate. CSilicon never alters guarded game files,
injects code, hooks functions, attaches a debugger during play, or attempts to
bypass VAC. A successful online test is evidence for that exact runtime and CS2
build, not a permanent guarantee.

## Primary sources

- [CS2 platform requirements](https://store.steampowered.com/app/730/CounterStrike_2/)
- [Steam for Linux hardware/software requirements](https://github.com/ValveSoftware/steam-for-linux/blob/master/README.md)
- [Apple: Intel binaries in ARM Linux VMs](https://developer.apple.com/documentation/virtualization/running-intel-binaries-in-linux-vms)
- [Apple: Linux VM Virtio GPU 2D](https://developer.apple.com/videos/play/wwdc2022/10002/)
- [Asahi: AAA gaming architecture](https://asahilinux.org/2024/10/aaa-gaming-on-asahi-linux/)
- [Asahi: M4 feature support](https://asahilinux.org/docs/platform/feature-support/m4/)
- [CrossOver CS2 compatibility](https://www.codeweavers.com/compatibility/crossover/counter-strike-global-offensive)
- [CodeWeavers anti-cheat support policy](https://support.codeweavers.com/anti-cheat)
- [FACEIT anti-cheat platform support](https://support.faceit.com/hc/es/articles/9394666828188--Qu%C3%A9-es-FACEIT-Anti-cheat-y-c%C3%B3mo-funciona)
